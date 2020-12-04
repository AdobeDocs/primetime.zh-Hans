---
description: TVSDK响应加载媒体项而调度媒体播放器项事件。
seo-description: TVSDK响应加载媒体项而调度媒体播放器项事件。
seo-title: 加载器事件
title: 加载器事件
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 加载器事件{#loader-events}

TVSDK响应加载媒体项而调度媒体播放器项事件。

这些事件提供了替代工作流。 创建MediaPlayer时，不需要实现此接口。 当您希望具有`MediaPlayerItemLoader`时使用此选项。

要获得与加载媒体播放器资源相关的事件通知，请注册`MediaPlayerItemLoader.LoaderListener`的实现，包括以下事件。

| 事件 | 意义 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerItemplayerItem) | 媒体资源加载已成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 加载媒体资源时出现问题。 |

>[!NOTE]
>
>另请参阅QoS事件下的`onLoadInfo (loadInfo)`。

