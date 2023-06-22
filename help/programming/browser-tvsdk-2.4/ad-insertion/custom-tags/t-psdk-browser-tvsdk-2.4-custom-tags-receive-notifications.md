---
description: 要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。
title: 为定时元数据通知添加侦听器
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 为定时元数据通知添加侦听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。

当新的 `TimedMetadata` 创建对象，MediaPlayer调度 `AdobePSDK.TimedMetadataEvent`.

1. 实施相应的侦听器。

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. 注册事件侦听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3元数据通过相同的 `Events.TimedMetadataEvent`. 您可以使用 `timedMetadata.type` 属性以区分TAG和ID3。
