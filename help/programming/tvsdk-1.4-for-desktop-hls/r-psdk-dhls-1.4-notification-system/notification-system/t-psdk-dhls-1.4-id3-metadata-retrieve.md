---
description: ID3标记提供有关音频或视频文件的信息，例如文件标题或艺人姓名。 检测HLS流中传输流(TS)区段级别的ID3标记并调度事件。 应用程序可以从标记中提取数据。
title: ID3标记
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# ID3标记{#id-tags}

ID3标记提供有关音频或视频文件的信息，例如文件标题或艺人姓名。 检测HLS流中传输流(TS)区段级别的ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可识别音频(AAC)和视频(H.264)流中的ID3元数据（版本2.3.0或2.4.0），以及任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不属于可识别版本或格式之一的ID3标记。 未指定的编码将被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出包含以下数据的通知：

* 信息代码= 303007
* 类型= ID3
* 名称=不存在
* ID = 0

1. 实施事件侦听器 `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` 并在 `MediaPlayer` 对象。

   TVSDK在检测到ID3元数据时调用此侦听器。

   >[!NOTE]
   >
   >自定义广告提示使用相同的 `onTimedMetadata` 指示检测到新标记的事件。 这不应导致任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关更多信息，请参阅custom-tags-configure 。

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
