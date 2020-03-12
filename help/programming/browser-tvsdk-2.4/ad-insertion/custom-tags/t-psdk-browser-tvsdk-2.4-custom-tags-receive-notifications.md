---
description: 要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。
seo-description: 要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。
seo-title: 为定时元数据通知添加监听器
title: 为定时元数据通知添加监听器
uuid: c82c5549-0ab6-4343-a766-5176e784d4cb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 为定时元数据通知添加监听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。

创建新 `TimedMetadata` 对象时，MediaPlayer将调度 `AdobePSDK.TimedMetadataEvent`。

1. 实现适当的监听器。

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. 注册事件监听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3元数据通过相同的方式调度 `Events.TimedMetadataEvent`。 您可以使用该 `timedMetadata.type` 属性来区分TAG和ID3。

