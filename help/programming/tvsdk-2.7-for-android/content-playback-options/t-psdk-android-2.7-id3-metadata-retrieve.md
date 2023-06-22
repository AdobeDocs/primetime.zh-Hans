---
description: ID3标记提供有关音频或视频文件的信息，例如文件标题或艺人姓名。 TVSDK在HLS流中的传输流(TS)区段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
title: ID3标记
exl-id: 316bc704-e71a-4fd7-b970-706b8c08a42e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# ID3标记 {#id-tags}

ID3标记提供有关音频或视频文件的信息，例如文件标题或艺人姓名。 TVSDK在HLS流中的传输流(TS)区段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可将其音频(AAC)和视频(H.264)流中的ID3元数据（版本2.3.0或2.4.0）识别为任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不属于可识别版本或格式之一的ID3标记。 未指定的编码将被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出包含以下数据的通知：

* 类型= ID3
* 名称= ID3

1. 实施事件侦听器 `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 并在 `MediaPlayer` 对象。

   TVSDK在检测到以下内容时调用此侦听器： `ID3` 元数据。

   >[!TIP]
   >
   >自定义广告提示使用相同的 `onTimedMetadata` 指示检测到新标记的事件。 这不应导致任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关更多信息，请参阅 [自定义标记](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


1. 检索元数据。

   ```java
   @Override 
    public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```
