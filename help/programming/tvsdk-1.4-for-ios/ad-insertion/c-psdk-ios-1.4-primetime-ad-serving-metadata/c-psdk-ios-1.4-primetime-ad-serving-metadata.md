---
description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-title: Primetime广告服务器元数据
title: Primetime广告服务器元数据
uuid: 314f14c0-4da4-4da6-96f9-5a5ffea22a99
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支持解析和插入用于VOD和实时／线性流的广告。

>[!NOTE]
>
>在视频内容中包含广告之前，请提供以下元数据信息：
>
>* A, `mediaID`它标识要播放的特定内容。
>* 您的 `zoneID`，它标识您的公司或网站。
>* 广告服务器域，它指定所分配广告服务器的域。
>* 其他定位参数。

>



## 设置Primetime广告服务器元数据 {#section_86C4A3B2DF124770B9B7FD2511394313}

您的应用程序必须向TVSDK提 `PTAuditudeMetadata` 供连接到广告服务器所需的信息。

设置广告服务器元数据：

1. 创建PTAuditudeMetadata [实例](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) ，并设置其属性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 使用将 `PTAuditudeMetadata` 实例设置为当前元数据 `PTMediaPlayerItem` 的元数据 `PTAdResolvingMetadataKey`。

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   以下是一个示例：

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

## 支持全事件重播广告 {#section_6016E1DAF03645C8A8388D03C6AB7571}

全事件重播(FER)是充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据／提示确定广告的放置位置。 但是，有时实时／线性内容可能与VOD内容类似。 例如，当实时内容完成时，将 `EXT-X-ENDLIST` 向实时清单附加一个标记。 对于HLS，标 `EXT-X-ENDLIST` 记表示流是VOD流。 TVSDK无法自动区分此流与普通VOD流，以正确插入广告。

您的应用程序必须通过指定内容来告诉TVSDK内容是实时的还是VOD `PTAdSignalingMode`。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告中断的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单读取所有提示点并转到广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

除了与提示点关联的每个请求外，TVSDK还对预放广告提出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使 `PTAdSignalingMode` 用指定 `PTAdMetadata.signalingMode`。

   有效值 `PTAdSignalingModeDefault`有 `PTAdSignalingModeManifestCues`、和 `PTAdSignalingModeServerMap`。

   在呼叫之前，必须设置广告信令模 `prepareToPlay`式。 在TVSDK开始解析广告并将其放在时间轴上后，将忽略对广告信号模式所做的更改。 为资源创建广告元数据时设置模式。

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

