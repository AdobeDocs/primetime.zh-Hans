---
description: 要接收有关清单中标记的通知，您需要实施适当的事件侦听器。
title: 为定时元数据通知添加侦听器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 为定时元数据通知添加侦听器 {#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，您需要实施适当的事件侦听器。

您可以通过侦听定时元数据 `onTimedMetadata`，用于通知应用程序相关活动。 每次在解析内容期间标识唯一订阅的标记时，TVSDK都会准备一个新的 `TimedMetadata` 对象并调度此事件。 对象包含您订阅的标记的名称、播放中将显示此标记的本地时间以及其他数据。

倾听事件。

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

ID3元数据使用相同的 `onTimedMetadata` 侦听器以指示存在ID3标记。 但是，这应该不会导致任何混淆，因为您可以使用 `TimedMetadata` `type` 属性，用于区分TAG和ID3。 有关ID3标记的详细信息，请参阅 [ID3标记](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).
