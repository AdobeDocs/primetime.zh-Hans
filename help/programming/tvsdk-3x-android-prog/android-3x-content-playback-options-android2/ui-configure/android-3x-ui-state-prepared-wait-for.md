---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
title: 等待有效状态
exl-id: bfd77163-7ca8-41e1-8b97-2d6a765f5ccd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 等待有效状态 {#wait-for-a-valid-status}

借助TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK提供了播放器实例上的方法和属性，您可以使用这些方法和属性来配置播放器用户界面。

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器未至少处于所需的状态，则许多播放器方法会引发 `MediaPlayerException`.

所需的状态通常为PREPARED。 发生此情况时，的回调例程 `StatusChangeEventListener.onStatusChanged()` 执行。

要确认状态为 `PREPARED`，检查 `MediaPlayer.MediaPlayerStatus`.
