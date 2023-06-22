---
description: TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲或搜寻。
title: QoS事件
exl-id: 0ccdaed1-1fce-46b7-b0f0-25e7ea98da86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲或搜寻。

要接收有关所有QoS相关事件的通知，请注册以下实施 `MediaPlayer.QOSEventListener` 包括以下回调：

| 事件 | 含义 |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | 缓冲完成。 |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | 已开始缓冲。 |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | 已成功下载片段。 |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification. [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) warning) | 发生了可恢复的错误。 |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustedTime) | 搜寻已完成。 |
| [onseekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | 正在开始搜寻。 |
