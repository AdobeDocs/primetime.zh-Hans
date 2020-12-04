---
description: 要接收有关清单中标记的通知，请实施相应的事件监听器。
seo-description: 要接收有关清单中标记的通知，请实施相应的事件监听器。
seo-title: 为定时元数据通知添加监听器
title: 为定时元数据通知添加监听器
uuid: cd7a5936-d63a-4711-ac16-2d79bac099a3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 为定时元数据通知添加监听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请实施相应的事件监听器。

您可以通过监听以下事件来监视定时元数据，这些活动会通知您的应用程序相关的：

* `onTimedMetadata`:每次在分析内容时识别唯一的订阅标记，TVSDK会准备一个新对 `TimedMetadata` 象并调度此事件。

   该对象包含您订阅的标记的名称、播放中显示此标记的本地时间以及其他数据。

   听事件。

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener =  
     new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
   
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() !=  
                      null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

ID3元数据使用相同的onTimedMetadata侦听器来指示ID3标记存在。 但是，这不会造成任何混淆，因为您可以使用`TimedMetadata`对象的`type`属性来区分TAG和ID3。 有关ID3标记的详细信息，请参阅[ID3标记](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md)。
