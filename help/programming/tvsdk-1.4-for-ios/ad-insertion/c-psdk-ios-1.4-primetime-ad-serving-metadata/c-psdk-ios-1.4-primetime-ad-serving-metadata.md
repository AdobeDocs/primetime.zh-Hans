---
description: TVSDK支持解析和插入VOD和实时/线性流的广告。
title: Primetime广告服务器元数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支持解析和插入VOD和实时/线性流的广告。

>[!NOTE]
>
>在视频内容中包含广告之前，请提供以下元数据信息：
>
>* A `mediaID`，用于标识要播放的特定内容。
>* 您的 `zoneID`，用于标识您的公司或网站。
>* 广告服务器域，用于指定所分配广告服务器的域。
>* 其他定位参数。
>

## 设置Primetime广告服务器元数据 {#section_86C4A3B2DF124770B9B7FD2511394313}

您的应用程序必须向TVSDK提供所需的 `PTAuditudeMetadata` 用于连接到ad服务器的信息。

设置广告服务器元数据：

1. 创建实例 [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) 并设置其属性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 设置 `PTAuditudeMetadata` 作为当前元数据的实例 `PTMediaPlayerItem` 元数据，使用 `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   示例如下：

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```

## 在全事件重放中启用广告 {#section_6016E1DAF03645C8A8388D03C6AB7571}

完整事件重放(FER)是一种充当实时/DVR资源的VOD资源，因此您的应用程序必须采取措施以确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据/提示来确定放置广告的位置。 但是，有时实时/线性内容可能与VOD内容类似。 例如，当实时内容结束时， `EXT-X-ENDLIST` 标记将附加到实时清单中。 对于HLS， `EXT-X-ENDLIST` 标记表示该流是VOD流。 TVSDK无法自动将此流与常规VOD流区分开来正确插入广告。

您的应用程序必须指定 `PTAdSignalingMode`.

对于FER流，Adobe Primetime ad decisioning服务器不应提供在开始播放之前需要在时间轴上插入的广告时间列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单中读取所有提示点，并且对于每个提示点转到广告服务器以请求广告时间。 此过程类似于实时/DVR内容。

除了与提示点关联的每个请求之外，TVSDK还会为前置广告提出额外的广告请求。

1. 从外部源（如vCMS）获取应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请指定 `PTAdSignalingMode` 通过使用 `PTAdMetadata.signalingMode`.

   有效值为 `PTAdSignalingModeDefault`， `PTAdSignalingModeManifestCues`、和 `PTAdSignalingModeServerMap`.

   在调用之前，必须设置广告信号模式 `prepareToPlay`. 在TVSDK开始解析广告并将广告放置到时间轴上后，对广告信号模式的更改将被忽略。 在为资源创建广告元数据时设置模式。

1. 继续播放。

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```
