---
description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-title: Primetime广告服务器元数据
title: Primetime广告服务器元数据
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 启用全事件重播{#section_6016E1DAF03645C8A8388D03C6AB7571}中的广告

全事件重播(FER)是充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据／提示确定广告的放置位置。 但是，有时实时／线性内容可能与VOD内容类似。 例如，当实时内容完成时，将向实时清单附加一个`EXT-X-ENDLIST`标记。 对于HLS,`EXT-X-ENDLIST`标记表示流是VOD流。 TVSDK无法自动区分此流与普通VOD流，以正确插入广告。

应用程序必须通过指定`PTAdSignalingMode`来告诉TVSDK内容是实时的还是VOD的。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告中断的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单读取所有提示点并转到广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

除了与提示点关联的每个请求外，TVSDK还对预放广告提出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使用`PTAdMetadata.signalingMode`指定`PTAdSignalingMode`。

   有效值为`PTAdSignalingModeDefault`、`PTAdSignalingModeManifestCues`和`PTAdSignalingModeServerMap`。

   在调用`prepareToPlay`之前，必须设置广告信令模式。 在TVSDK开始解析广告并将其放在时间轴上后，将忽略对广告信号模式所做的更改。 为资源创建广告元数据时设置模式。

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
