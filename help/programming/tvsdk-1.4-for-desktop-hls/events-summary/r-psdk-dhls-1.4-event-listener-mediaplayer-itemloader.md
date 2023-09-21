---
description: TVSDK调度媒体播放器项目事件以响应加载媒体项目。
title: 加载器事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 加载器事件{#loader-events}

TVSDK调度媒体播放器项目事件以响应加载媒体项目。

这些事件提供了替代工作流。 创建时，无需实施此接口 `MediaPlayer`. 当您想要拥有 `MediaPlayerItemLoader`.

要收到与加载媒体播放器资源相关的事件通知，请在注册以下事件的侦听器 `MediaPlayerItemLoader` 对象。

| 事件 | 含义 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒体资源加载已成功完成。 |
| MediaPlayerItemLoader。[失败](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 加载媒体资源时出现问题。 |
