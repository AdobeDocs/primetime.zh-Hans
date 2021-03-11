---
description: 要接收有关清单中标记的通知，请注册相应的事件侦听器。
title: 为定时元数据通知添加侦听器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 为定时元数据通知添加侦听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请注册相应的事件侦听器。

您可以通过侦听以下事件来监视计时元数据，这些活动会向您的应用程序通知相关的元数据：

* `MediaPlayerItemEvent.ITEM_CREATED`:在创建对象 `TimedMetadata` 后，可以使用对象 `MediaPlayerItem` 的初始列表。

   此事件会在发生此情况时通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`:对于清单/播放列表定期刷新的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此可 `TimedMetadata` 能会向属性添加其他 `MediaPlayerItem.timedMetadata` 对象。

   此事件会在发生此情况时通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次创建新 `TimedMetadata` 对象时，MediaPlayer都会调度此事件。

   不为在初始化阶段创建的`TimedMetadata`对象调度此事件。

1. 实施适当的监听器。

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

1. 注册事件监听器。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

ID3元数据通过相同的`TimedMetadataEvent.TIMED_METADATA_AVAILABLE`进行调度。 但是，这不会造成任何混淆，因为您可以使用TimedMetadata对象的`type`属性区分TAG和ID3。 有关ID3标记的详细信息，请参阅[ID3标记](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md)。