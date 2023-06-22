---
description: 您可以决定是仅解析出现在用户当前实时点之后的广告，还是解析出现在当前实时点之前的广告。
title: 为DVR窗口加载广告
exl-id: 3e8542a8-0912-4023-904d-0fdb28411a9d
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 为DVR窗口加载广告 {#load-ad-for-a-dvr-window}

您可以决定是仅解析出现在用户当前实时点之后的广告，还是解析出现在当前实时点之前的广告。

当用户开始查看DVR流开头的内容时，TVSDK会解析该流当时的所有广告。 但是，当用户开始查看流开始后的某个时间点上的内容时，您可以决定是仅解析在用户当前实时点之后发生的广告，还是同时解析在当前实时点之前发生的广告。

>[!TIP]
>
>在当前实时点之后解析广告的速度更快，但如果用户向后搜索，则此选项会阻止播放器播放之前显示的广告。

## DVR窗口的控制和加载 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

要控制DVR窗口的广告加载，请执行以下操作：

要为整个流加载所有广告，请将 `PTAdMetadata.enableDVRAds` 属性至 `YES`.

>[!NOTE]
>
>默认值为 `NO`，并且此选项仅从当前实时点加载广告。

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
