---
description: 要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。
title: 为定时元数据通知添加侦听器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# 为定时元数据通知添加侦听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请侦听AdobePSDK.TimedMetadataEvent。

创建新`TimedMetadata`对象时，MediaPlayer将调度`AdobePSDK.TimedMetadataEvent`。

1. 实施适当的监听器。

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

ID3元数据通过相同的`Events.TimedMetadataEvent`进行调度。 可以使用`timedMetadata.type`属性区分TAG和ID3。

