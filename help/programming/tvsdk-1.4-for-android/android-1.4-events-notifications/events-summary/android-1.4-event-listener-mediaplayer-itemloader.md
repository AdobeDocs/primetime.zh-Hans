---
description: TVSDK调度媒体播放器项目事件以响应加载媒体项目。
title: 加载器事件
exl-id: 80a503f2-ad2e-44e5-93dc-2311df77f52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 加载器事件{#loader-events}

TVSDK调度媒体播放器项目事件以响应加载媒体项目。

这些事件提供了一个替代工作流。 创建MediaPlayer时，您无需实施此接口。 当您希望使用 `MediaPlayerItemLoader`.

要收到与加载媒体播放器资源相关的事件的通知，请注册以下实施 `MediaPlayerItemLoader.LoaderListener` 包括以下活动。

| 事件 | 含义 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒体资源加载已成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 加载媒体资源时出现问题。 |

>[!NOTE]
>
>另请参阅 `onLoadInfo (loadInfo)` 在QoS事件下。
