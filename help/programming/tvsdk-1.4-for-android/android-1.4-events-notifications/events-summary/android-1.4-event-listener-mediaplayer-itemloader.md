---
description: TVSDK调度媒体播放器项目事件以响应加载媒体项目。
title: 加载器事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 加载器事件{#loader-events}

TVSDK调度媒体播放器项目事件以响应加载媒体项目。

这些事件提供了替代工作流。 创建MediaPlayer时，您无需实施此接口。 当您想要拥有 `MediaPlayerItemLoader`.

要收到与加载媒体播放器资源相关的事件的通知，请注册以下实施 `MediaPlayerItemLoader.LoaderListener` 包括以下活动。

| 事件 | 含义 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒体资源加载已成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 加载媒体资源时出现问题。 |

>[!NOTE]
>
>另请参阅 `onLoadInfo (loadInfo)` 在QoS事件下。
