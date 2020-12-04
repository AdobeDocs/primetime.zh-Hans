---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-title: 等待有效状态
title: 等待有效状态
uuid: ad9df366-c443-4e6b-a7ab-658d5691eb94
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 等待有效状态{#wait-for-a-valid-state}

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

玩家在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不至少处于所需状态，则许多播放器方法会抛出`IllegalStateException`。

所需的状态通常为`PTMediaPlayerStatusReady`。