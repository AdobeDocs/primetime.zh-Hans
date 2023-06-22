---
description: 要接收有关清单中标记的通知，请实施相应的事件侦听器。
title: 为定时元数据通知添加侦听器
exl-id: febf354b-2a25-4108-abd9-6ff1e09cee39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 为定时元数据通知添加侦听器 {#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请实施相应的事件侦听器。

您可以通过侦听以下事件来监视定时元数据，这些事件会通知您的应用程序相关活动：

* `onTimedMetadata`：在分析内容期间，每次标识唯一的订阅标记时，TVSDK都会准备一个新的 `TimedMetadata` 对象并调度此事件。

   对象包含您订阅的标记的名称、播放中将显示此标记的本地时间以及其他数据。

   听听事件。

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

ID3元数据使用相同的onTimedMetadata侦听器来指示存在ID3标记。 但是，这应该不会导致任何混淆，因为您可以使用 `TimedMetadata` 对象的 `type` 属性，用于区分TAG和ID3。 有关ID3标记的详细信息，请参阅 [ID3标记](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
