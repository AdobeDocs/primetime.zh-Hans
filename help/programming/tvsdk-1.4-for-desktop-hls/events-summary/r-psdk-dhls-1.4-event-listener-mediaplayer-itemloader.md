---
description: TVSDK响应加载媒体项而调度媒体播放器项事件。
seo-description: TVSDK响应加载媒体项而调度媒体播放器项事件。
seo-title: 加载器事件
title: 加载器事件
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 加载器事件{#loader-events}

TVSDK响应加载媒体项而调度媒体播放器项事件。

这些事件提供了替代工作流。 创建时，您无需实现此接口 `MediaPlayer`。 当您想要购买时使用它 `MediaPlayerItemLoader`。

要获得与加载媒体播放器资源相关的事件的通知，请向对象注册以下事件的监听 `MediaPlayerItemLoader` 器。

| 活动 | 意义 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒体资源加载成功完成。 |
| MediaPlayerItemLoader。[失败](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 加载媒体资源时出现问题。 |