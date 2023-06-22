---
description: 要接收有关清单中标记的通知，请注册相应的事件侦听器。
title: 为定时元数据通知添加侦听器
exl-id: 1df8a4fc-8368-4a80-8f8b-00c1207e6602
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 为定时元数据通知添加侦听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请注册相应的事件侦听器。

您可以通过侦听以下事件来监视定时元数据，这些事件会通知您的应用程序相关活动：

* `MediaPlayerItemEvent.ITEM_CREATED`：初始列表 `TimedMetadata` 对象在以下位置后可用： `MediaPlayerItem` 创建。

   发生此情况时，此事件会通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`：对于清单/播放列表定期刷新的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此额外 `TimedMetadata` 对象可以添加到 `MediaPlayerItem.timedMetadata` 属性。

   发生此情况时，此事件会通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`：每次 `TimedMetadata` 创建对象，此事件由MediaPlayer调度。

   此事件不会分派给 `TimedMetadata` 在初始化阶段创建的对象。

1. 实施相应的侦听器。

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. 注册事件侦听器。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

ID3元数据通过相同的 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. 但是，这不会造成任何混淆，因为您可以使用TimedMetadata对象的 `type` 属性，用于区分TAG和ID3。 有关ID3标记的详细信息，请参阅 [ID3标记](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
