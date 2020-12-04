---
description: 通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。
seo-description: 通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。
seo-title: 等待有效状态
title: 等待有效状态
uuid: 22b68162-1625-4e8a-8566-b0c198155622
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# 等待有效状态{#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。

在您使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
玩家在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器至少不处于所需状态，许多播放器方法会抛出`IllegalStateException`。

所需的状态通常为PREPARED。
