---
description: 您的应用程序必须在适当的时间使用相应的TimedMetadata对象。
seo-description: 您的应用程序必须在适当的时间使用相应的TimedMetadata对象。
seo-title: 在调度时存储定时元数据对象
title: 在调度时存储定时元数据对象
uuid: 3d0ed022-829d-474e-83a9-152caeb5b317
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 在调度定时元数据对象时存储这些对象{#store-timed-metadata-objects-as-they-are-dispatched}

您的应用程序必须在适当的时间使用相应的TimedMetadata对象。

在内容分析（在播放前发生）期间，TVSDK识别订阅的标记并通知您的应用程序这些标记。

>[!TIP]
>
>与每个`TimedMetadata`关联的时间是播放时间线上的本地时间。

要在调度时存储定时元数据对象，请执行以下操作：

1. 跟踪当前播放时间。
1. 将当前播放时间与所调度的`TimedMetadata`对象匹配。

1. 使用`TimedMetadata`，其中开始时间等于当前本地播放时间。

   以下示例说明如何在`ArrayList`中保存`TimedMetadata`对象。

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

