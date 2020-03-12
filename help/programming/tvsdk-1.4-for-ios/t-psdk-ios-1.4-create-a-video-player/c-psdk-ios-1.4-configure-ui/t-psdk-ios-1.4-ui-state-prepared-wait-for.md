---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-title: 等待有效状态
title: 等待有效状态
uuid: e13201d7-b217-4d01-bdb7-a71855e3500e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 等待有效状态{#wait-for-a-valid-state}

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

玩家在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不至少处于所需状态，将引发许多播放器方法 `IllegalStateException`。

通常情况下为必需状态 `PTMediaPlayerStatusReady`。
