---
description: 在使用自定义广告标记时，您可以覆盖TVSDK如何搜索广告的默认行为。
title: 控制通过自定义广告标记进行搜索的播放行为
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 控制搜索自定义广告标记的播放行为{#control-playback-behavior-for-seeking-over-custom-ad-markers}

在使用自定义广告标记时，您可以覆盖TVSDK如何搜索广告的默认行为。

默认情况下，当用户在放置自定义广告标记后搜索或查看过去的广告部分时，TVSDK会跳过广告。 这可能与标准广告中断的当前播放行为不同。

当用户搜索超过一个或多个自定义广告时，您可以告诉TVSDK将播放头重新定位到最近跳过的自定义广告的开头。

1. 将`DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED`明细列表设置为字符串值“true”（不是布尔`true`）的Metadata实例进行配置。

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

