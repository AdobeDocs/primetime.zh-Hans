---
description: TVSDK支持解析和插入VOD和实时/线性流的广告。
title: Primetime广告服务器元数据
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# 概述{#primetime-ad-server-metadata-overview}

TVSDK支持解析和插入VOD和实时/线性流的广告。

>[!NOTE]
>
>在视频内容中包含广告之前，请提供以下元数据信息：
>
>* `mediaID`，用于标识要播放的特定内容。
>* 您的`zoneID`，用于标识您的公司或网站。
>* 您的广告服务器域，它指定您分配的广告服务器的域。
>* 其他定位参数。

>



## 设置Primetime广告服务器元数据{#section_86C4A3B2DF124770B9B7FD2511394313}

您的应用程序必须向TVSDK提供连接到广告服务器所需的`PTAuditudeMetadata`信息。

设置广告服务器元数据：

1. 创建[PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html)的实例并设置其属性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 使用`PTAdResolvingMetadataKey`将`PTAuditudeMetadata`实例设置为当前`PTMediaPlayerItem`元数据的元数据。

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

## 启用全事件重播{#section_6016E1DAF03645C8A8388D03C6AB7571}中的广告

全事件重播(FER)是一个VOD资产，充当实时/DVR资产，因此您的应用程序必须采取步骤以确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据/提示确定放广告的位置。 但是，有时实时/线性内容可能与VOD内容相似。 例如，当活动内容完成时，将向活动清单附加一个`EXT-X-ENDLIST`标记。 对于HLS，`EXT-X-ENDLIST`标记表示流是VOD流。 TVSDK无法自动区分此流与普通VOD流，以正确插入广告。

应用程序必须通过指定`PTAdSignalingMode`来告诉TVSDK内容是实时的还是VOD的。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告中断的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单读取所有提示点并转到每个提示点的广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

除了与提示点关联的每个请求外，TVSDK还对前放广告发出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使用`PTAdMetadata.signalingMode`指定`PTAdSignalingMode`。

   有效值为`PTAdSignalingModeDefault`、`PTAdSignalingModeManifestCues`和`PTAdSignalingModeServerMap`。

   在调用`prepareToPlay`之前，必须设置广告信令模式。 在TVSDK开始解析广告并将其放置到时间轴上后，将忽略对广告信号模式的更改。 在为资源创建广告元数据时设置模式。

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

