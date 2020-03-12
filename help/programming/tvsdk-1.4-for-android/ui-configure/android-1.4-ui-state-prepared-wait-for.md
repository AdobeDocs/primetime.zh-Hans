---
description: 通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。
seo-description: 通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。
seo-title: 等待有效状态
title: 等待有效状态
uuid: 22b68162-1625-4e8a-8566-b0c198155622
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 等待有效状态 {#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
播放器在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不处于至少所需的状态，将引发许多播放器方法 `IllegalStateException`。

所需状态通常为PREPARED。
