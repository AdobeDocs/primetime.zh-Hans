---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
title: 等待有效的状态
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 等待有效的状态{#wait-for-a-valid-state}

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

播放器会通过各种状态进行移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器未至少处于所需的状态，则许多播放器方法会引发 `IllegalStateException`.

所需的状态通常为 `PTMediaPlayerStatusReady`.
