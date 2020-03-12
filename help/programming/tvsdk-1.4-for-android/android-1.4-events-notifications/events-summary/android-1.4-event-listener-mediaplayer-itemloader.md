---
description: TVSDK响应加载媒体项而调度媒体播放器项事件。
seo-description: TVSDK响应加载媒体项而调度媒体播放器项事件。
seo-title: 加载器事件
title: 加载器事件
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 加载器事件{#loader-events}

TVSDK响应加载媒体项而调度媒体播放器项事件。

这些事件提供了替代工作流。 在创建MediaPlayer时，不需要实现此接口。 当您想要购买时使用它 `MediaPlayerItemLoader`。

要获得与加载媒体播放器资源相关的事件的通知，请注册包括以 `MediaPlayerItemLoader.LoaderListener` 下事件的实现。

| 活动 | 意义 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒体资源加载成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 加载媒体资源时出现问题。 |

>[!NOTE]
>
>另请参 `onLoadInfo (loadInfo)` 阅QoS事件下。

