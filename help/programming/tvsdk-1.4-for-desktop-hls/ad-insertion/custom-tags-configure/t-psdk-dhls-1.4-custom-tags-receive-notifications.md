---
description: 要接收有关清单中标记的通知，请注册相应的事件侦听器。
title: 为定时元数据通知添加侦听器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 为定时元数据通知添加侦听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请注册相应的事件侦听器。

您可以通过侦听以下事件来监视定时元数据，这些事件会通知您的应用程序相关活动：

* `MediaPlayerItemEvent.ITEM_CREATED`：初始列表 `TimedMetadata` 对象在以下时段后可用： `MediaPlayerItem` 创建。

  此事件会在发生这种情况时通知应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`：对于清单/播放列表定期刷新的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此也会显示 `TimedMetadata` 对象可添加到 `MediaPlayerItem.timedMetadata` 属性。

  此事件会在发生这种情况时通知应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`：每次使用 `TimedMetadata` 创建对象后，此事件将由MediaPlayer调度。

  此事件不会分派给 `TimedMetadata` 在初始化阶段创建的对象。

1. 实施相应的监听程序。

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

ID3元数据通过相同的来调度 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. 但是，这应该不会造成任何混淆，因为您可以使用TimedMetadata对象的 `type` 属性，用于区分TAG和ID3。 有关ID3标记的详细信息，请参阅 [ID3标记](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
