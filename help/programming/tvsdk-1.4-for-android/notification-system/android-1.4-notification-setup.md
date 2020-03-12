---
description: 您可以侦听通知，也可以向通知历史记录添加您自己的通知。
seo-description: 您可以侦听通知，也可以向通知历史记录添加您自己的通知。
seo-title: 设置通知系统
title: 设置通知系统
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 设置通知系统{#set-up-your-notification-system}

您可以侦听通知，也可以向通知历史记录添加您自己的通知。

Primetime Player通知系统的核心是类， `Notification` 它表示独立通知。

类提 `NotificationHistory` 供了累积通知的机制。 它存储表示通知集合的通知日志(NotificationHistoryItem)对象。

接收通知：

* 侦听通知
* 向通知历史记录添加通知

1. 侦听状态更改。
1. 实现回 `MediaPlayer.PlaybackEventListener.onStateChanged` 调。
1. TVSDK将两个参数传递给回调：

   * 新状态( `MediaPlayer.PlayerState`)
   * 对 `MediaPlayerNotification` 象

