---
description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-title: ID3标记
title: ID3标记
uuid: 5e5c5f89-7653-47c1-b9c1-6b9b9b1f8d73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# ID3标记 {#id-tags}

ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可以在音频(AAC)和视频(H.264)流中识别ID3元数据（版本2.3.0或2.4.0），并使用其任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不属于某个可识别的版本或格式的ID3标记。 未指定编码被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出一条通知，其中包含以下数据：

* InfoCode = 303007
* 类型= ID3
* 名称=不存在
* ID = 0

1. 为实现事件监听器， `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 并向对象注册该事 `MediaPlayer` 件监听器。

   TVSDK在检测到ID3元数据时调用此监听器。

   >[!NOTE]
   >
   >自定义广告提示使用相 `onTimedMetadata` 同的事件指示检测新标记。 这不应造成任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关详细信息，请参阅custom-tags-configure。

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
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```

