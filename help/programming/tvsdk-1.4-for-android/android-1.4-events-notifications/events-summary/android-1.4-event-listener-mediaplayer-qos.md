---
description: TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲或搜索。
seo-description: TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲或搜索。
seo-title: QoS事件
title: QoS事件
uuid: 27f60cd3-d3fc-4ea3-81df-96d0fe9f7068
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# QoS事件{#qos-events}

TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲或搜索。

要获得所有QoS相关事件的通知，请注册以下回 `MediaPlayer.QOSEventListener` 呼的实现：

| 活动 | 意义 |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | 缓冲完成。 |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | 缓冲已开始。 |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | 已成功下载片段。 |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification)。 [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) ) | 发生可恢复错误。 |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustedTime) | 搜索已完成。 |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | 搜索即将开始。 |