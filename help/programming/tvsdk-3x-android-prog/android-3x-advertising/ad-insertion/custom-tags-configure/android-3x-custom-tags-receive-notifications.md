---
description: 要接收有关清单中标记的通知，您需要实施相应的事件监听器。
seo-description: 要接收有关清单中标记的通知，您需要实施相应的事件监听器。
seo-title: 为定时元数据通知添加监听器
title: 为定时元数据通知添加监听器
uuid: bb996b4a-282e-4321-a9e9-513f0df45b70
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 为定时元数据通知添加监听器 {#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，您需要实施相应的事件监听器。

您可以通过监听来监视定时元数据， `onTimedMetadata`这会向应用程序通知相关活动。 每次在分析内容时识别唯一的订阅标记时，TVSDK都会准备一个新对象并 `TimedMetadata` 调度此事件。 该对象包含您订阅的标记的名称、播放中显示此标记的本地时间以及其他数据。

聆听活动。

```java
private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
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
        } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
            displayRanges(); 
        } 
    } 
}; 
```

ID3元数据使用同一 `onTimedMetadata` 个监听器来指示ID3标记的存在。 但是，这不应引起任何混淆，因为您可以使 `TimedMetadata` 用属 `type` 性区分TAG和ID3。 有关ID3标记的详细信息，请参 [阅ID3标记](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md)。