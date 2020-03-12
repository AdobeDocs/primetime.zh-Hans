---
description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-title: ID3标记
title: ID3标记
uuid: 5c016260-5ced-480e-897a-11ffe7f34441
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# ID3标记{#id-tags}

ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可以在音频(AAC)和视频(H.264)流中识别ID3元数据（版本2.3.0或2.4.0），并使用其任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不属于某个可识别的版本或格式的ID3标记。 未指定编码被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出一条通知，其中包含以下数据：

* InfoCode = 303007
* 类型= ID3
* 名称=不存在
* ID = 0

1. 为实现事件监听器， `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` 并向对象注册该事 `MediaPlayer` 件监听器。

   TVSDK在检测到ID3元数据时调用此监听器。

   >[!NOTE]
   >
   >自定义广告提示使用相 `onTimedMetadata` 同的事件指示检测新标记。 这不应造成任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关详细信息，请参阅custom-tags-configure。

1. 检索元数据。

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```

