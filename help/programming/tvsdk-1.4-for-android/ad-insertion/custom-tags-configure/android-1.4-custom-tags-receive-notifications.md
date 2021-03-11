---
description: 要接收有关清单中标签的通知，请实施适当的事件侦听器。
title: 为定时元数据通知添加侦听器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 为定时元数据通知{#add-listeners-for-timed-metadata-notifications}添加侦听器

要接收有关清单中标签的通知，请实施适当的事件侦听器。

您可以通过侦听以下事件来监视计时元数据，这些活动会向您的应用程序通知相关的元数据：

* `onTimedMetadata`:每次在分析内容时识别唯一的订阅标记时，TVSDK会准备一个新对 `TimedMetadata` 象并调度此事件。

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

ID3元数据使用相同的onTimedMetadata侦听器来指示ID3标记的存在。 但是，这不会造成任何混淆，因为您可以使用`TimedMetadata`对象的`type`属性来区分TAG和ID3。 有关ID3标记的详细信息，请参阅[ID3标记](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md)。
