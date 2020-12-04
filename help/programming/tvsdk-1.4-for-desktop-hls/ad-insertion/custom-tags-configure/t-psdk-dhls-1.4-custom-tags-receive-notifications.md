---
description: 要接收清单中标记的通知，请注册相应的事件监听器。
seo-description: 要接收清单中标记的通知，请注册相应的事件监听器。
seo-title: 为定时元数据通知添加监听器
title: 为定时元数据通知添加监听器
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 为定时元数据通知添加监听器{#add-listeners-for-timed-metadata-notifications}

要接收清单中标记的通知，请注册相应的事件监听器。

您可以通过监听以下事件来监视定时元数据，这些活动会通知您的应用程序相关的：

* `MediaPlayerItemEvent.ITEM_CREATED`:对象的初始 `TimedMetadata` 列表在创建后 `MediaPlayerItem` 可用。

   此事件会在发生此情况时通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`:对于清单／播放列表定期刷新的实时／线性流，更新的播放列表／清单中可能显示其他自定义标记， `TimedMetadata` 因此可能会向属性添加其 `MediaPlayerItem.timedMetadata` 他对象。

   此事件会在发生此情况时通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次创建新 `TimedMetadata` 对象时，MediaPlayer都会调度此事件。

   对于在初始化阶段创建的`TimedMetadata`对象，不调度此事件。

1. 实现适当的监听器。

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

ID3元数据通过同一`TimedMetadataEvent.TIMED_METADATA_AVAILABLE`调度。 但是，这不会造成任何混淆，因为您可以使用TimedMetadata对象的`type`属性区分TAG和ID3。 有关ID3标记的详细信息，请参阅[ID3标记](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md)。