---
description: 您可以决定是仅解决用户当前活动点之后出现的广告，还是还要解决当前活动点之前出现的广告。
title: 为DVR窗口加载广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# 为DVR窗口{#load-ad-for-a-dvr-window}加载广告

您可以决定是仅解决用户当前活动点之后出现的广告，还是还要解决当前活动点之前出现的广告。

当用户开始在DVR流开始时视图内容时，TVSDK将解析当时该流的所有广告。 但是，当用户开始在流开始后的某个点视图内容时，您可以决定是仅解析在用户当前直播点之后出现的广告，还是还要解析在当前直播点之前出现的广告。

>[!TIP]
>
>在当前实时点之后解析广告速度更快，但如果用户向后搜索，则此选项会阻止播放器播放之前显示的广告。

## 控制DVR窗口{#section_2D93E2E947644D66B6F6ED1DD6742C25}的广告加载

要控制DVR窗口的广告加载，请执行以下操作：

    要加载整个流的所有广告，请将“PTAdMetadata.enableDVRAds”属性设置为“YES”。

>[!NOTE]
>
>默认值为`NO`，此选项仅从当前实时点加载广告。

例如：

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```
