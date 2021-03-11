---
description: 应用程序必须在适当的时间使用适当的TimedMetadata对象。
title: 在调度时存储定时元数据对象
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# 在调度定时元数据对象时存储这些对象{#store-timed-metadata-objects-as-they-are-dispatched}

应用程序必须在适当的时间使用适当的TimedMetadata对象。

在内容分析（在播放前发生）期间，TVSDK识别订阅的标记并通知您的应用程序这些标记。

>[!TIP]
>
>与每个`TimedMetadata`关联的时间是播放时间线上的本地时间。

要在调度时存储定时元数据对象，请执行以下操作：

1. 跟踪当前播放时间。
1. 将当前播放时间与调度的`TimedMetadata`对象匹配。

1. 使用`TimedMetadata`，其中开始时间等于当前本地播放时间。

   以下示例说明如何将`TimedMetadata`对象保存在`ArrayList`中。

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

