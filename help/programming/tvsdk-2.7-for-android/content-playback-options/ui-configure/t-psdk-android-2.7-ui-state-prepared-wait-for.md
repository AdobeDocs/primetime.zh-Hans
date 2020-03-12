---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
seo-title: 等待有效状态
title: 等待有效状态
uuid: ffa63ad6-84d3-4eb2-aa99-026418d86528
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 等待有效状态 {#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。

在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不至少处于所需状态，将引发许多播放器方法 `MediaPlayerException`。

所需的状态通常为PREPARED。 发生这种情况时，将执行回调例 `StatusChangeEventListener.onStatusChanged()` 程。

1. 要确认状态为，请 `PREPARED`选中 `MediaPlayer.MediaPlayerStatus`。
