---
description: 在使用自定义广告标记时，您可以覆盖TVSDK如何搜索广告的默认行为。
seo-description: 在使用自定义广告标记时，您可以覆盖TVSDK如何搜索广告的默认行为。
seo-title: 控制用于搜索自定义广告标记的播放行为
title: 控制用于搜索自定义广告标记的播放行为
uuid: cf973caf-be29-46ce-bfa4-651e7653f8d4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 控制搜索自定义广告标记的播放行为{#control-playback-behavior-for-seeking-over-custom-ad-markers}

在使用自定义广告标记时，您可以覆盖TVSDK如何搜索广告的默认行为。

默认情况下，当用户搜索或通过放置自定义广告标记所产生的广告部分时，TVSDK会跳过广告。 这可能与标准广告中断的当前播放行为不同。

当用户搜索超过一个或多个自定义广告时，您可以告诉TVSDK将播放头重新定位到最近跳过的自定义广告的开头。

1. 将`DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED`明细列表设置为字符串值“true”（不是布尔`true`）时配置元数据实例。

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. 创建并配置`MediaResource`实例，将其他配置选项传递给`TimeRangeCollection.toMetadata`。 此方法通过另一个通用元数据结构接收其他配置选项。

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

