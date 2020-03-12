---
description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-title: ID3标记
title: ID3标记
uuid: 96901223-81c7-49c7-bacf-7b4bbdff1691
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# ID3标记 {#id-tags}

ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可以识别音频(AAC)和视频(H.264)流中的ID3元数据（版本2.3.0或2.4.0），这些元数据采用其任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不属于某个可识别的版本或格式的ID3标记。 未指定编码被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出一条通知，其中包含以下数据：

* 类型= ID3
* 名称= ID3

1. 为实现事件监听器， `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 并向对象注册该事 `MediaPlayer` 件监听器。

   TVSDK在检测到元数据时调用此监 `ID3` 听器。

   >[!TIP]
   >
   >自定义广告提示使用相 `onTimedMetadata` 同的事件指示检测新标记。 这不应造成任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关详细信息，请参阅自 [定义标记](../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/custom-tags-configure/android-3x-custom-tags-configure.md)。

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
