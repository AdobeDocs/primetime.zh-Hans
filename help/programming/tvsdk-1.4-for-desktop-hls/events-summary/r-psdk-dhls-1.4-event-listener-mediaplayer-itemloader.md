---
description: TVSDK调度媒体播放器项目事件以响应加载媒体项目。
title: 加载器事件
exl-id: ee5be2d4-5c77-4af4-b8fe-8cef18d7c0d9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 加载器事件{#loader-events}

TVSDK调度媒体播放器项目事件以响应加载媒体项目。

这些事件提供了一个替代工作流。 创建 `MediaPlayer`. 当您希望使用 `MediaPlayerItemLoader`.

要收到与加载媒体播放器资源相关的事件的通知，请使用 `MediaPlayerItemLoader` 对象。

| 事件 | 含义 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒体资源加载已成功完成。 |
| MediaPlayerItemLoader。[失败](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 加载媒体资源时出现问题。 |
