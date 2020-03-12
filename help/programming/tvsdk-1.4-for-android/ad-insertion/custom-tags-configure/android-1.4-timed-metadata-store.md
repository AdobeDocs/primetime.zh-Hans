---
description: 您的应用程序必须在适当的时间使用相应的TimedMetadata对象。
seo-description: 您的应用程序必须在适当的时间使用相应的TimedMetadata对象。
seo-title: 在调度定时元数据对象时存储这些对象
title: 在调度定时元数据对象时存储这些对象
uuid: 0e6d2a42-37a8-477e-b925-66bbc23445c1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在调度定时元数据对象时存储这些对象 {#store-timed-metadata-objects-as-they-are-dispatched}

您的应用程序必须在适当的时间使用相应的TimedMetadata对象。

在内容分析（在播放前发生）期间，TVSDK会识别订阅的标记并通知您的应用程序这些标记。 与每个时间关联的时间 `TimedMetadata` 是播放时间线上的本地时间。

应用程序必须完成以下任务：

1. 跟踪当前播放时间。
1. 将当前播放时间与调度的对象匹 `TimedMetadata` 配。

1. 使用 `TimedMetadata` 开始时间等于当前本地播放时间的位置。

   以下示例演示如何将对 `TimedMetadata` 象保存到 `ArrayList`。

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

