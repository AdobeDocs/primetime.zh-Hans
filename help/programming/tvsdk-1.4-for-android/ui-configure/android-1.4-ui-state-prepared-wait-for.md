---
description: 通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK提供了播放器实例上的方法和属性，您可以使用这些方法和属性来配置播放器用户界面。
title: 等待有效的状态
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 等待有效的状态 {#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK提供了播放器实例上的方法和属性，您可以使用这些方法和属性来配置播放器用户界面。

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
播放器会经历各种状态。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器未至少处于所需的状态，则许多播放器方法会引发 `IllegalStateException`.

所需的状态通常为PREPARED。
