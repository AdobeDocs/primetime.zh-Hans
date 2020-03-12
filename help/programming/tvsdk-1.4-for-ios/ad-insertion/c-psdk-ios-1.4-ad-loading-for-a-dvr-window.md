---
description: 您可以决定是仅解析用户当前实时点之后发生的广告，还是还是要解析在当前实时点之前发生的广告。
seo-description: 您可以决定是仅解析用户当前实时点之后发生的广告，还是还是要解析在当前实时点之前发生的广告。
seo-title: 为DVR窗口加载广告
title: 为DVR窗口加载广告
uuid: 67bc3924-3d17-4d1a-b9a7-be8d0488a970
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 为DVR窗口加载广告 {#load-ad-for-a-dvr-window}

您可以决定是仅解析用户当前实时点之后发生的广告，还是还是要解析在当前实时点之前发生的广告。

当用户在DVR流的开始处开始查看内容时，TVSDK会解析当时该流的所有广告。 但是，当用户在流开始后的某个点开始查看内容时，您可以决定是仅解析用户当前实时点之后发生的广告，还是还要解析在当前实时点之前发生的广告。

>[!TIP]
>
>在当前实时点后解析广告速度更快，但如果用户向后搜索，则此选项会阻止玩家播放先前显示的广告。

## 控制DVR窗口的广告加载 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

要控制DVR窗口的广告加载，请执行以下操作：

要加载整个流的所有广告，请将属性 `PTAdMetadata.enableDVRAds` 设置为 `YES`。

>[!NOTE]
>
>默认值为， `NO`此选项仅从当前实时点加载广告。

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
