---
description: 您的应用程序必须在适当的时间使用适当的TimedMetadata对象。
title: 在调度定时元数据对象时存储这些对象
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 在调度定时元数据对象时存储这些对象 {#store-timed-metadata-objects-as-they-are-dispatched}

您的应用程序必须在适当的时间使用适当的TimedMetadata对象。

在播放之前进行的内容解析期间，TVSDK会识别订阅的标记并通知您的应用程序这些标记。

>[!TIP]
>
>与每个报表关联的时间 `TimedMetadata` 是播放时间轴上的本地时间。

要在调度定时元数据对象时存储这些对象，请执行以下操作：

1. 跟踪当前播放时间。
1. 将当前播放时间与调度的播放时间相匹配 `TimedMetadata` 对象。

1. 使用 `TimedMetadata` 其中开始时间等于当前本地播放时间。

   以下示例显示如何保存 `TimedMetadata` 中的对象 `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```
