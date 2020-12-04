---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-title: 等待有效状态
title: 等待有效状态
uuid: e13201d7-b217-4d01-bdb7-a71855e3500e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 等待有效状态{#wait-for-a-valid-state}

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

玩家在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不至少处于所需状态，则许多播放器方法会抛出`IllegalStateException`。

所需的状态通常为`PTMediaPlayerStatusReady`。
