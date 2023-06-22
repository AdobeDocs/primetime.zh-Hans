---
description: 您可以监听通知，也可以将您自己的通知添加到通知历史记录中。
title: 设置通知系统
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 设置通知系统{#set-up-your-notification-system}

您可以监听通知，也可以将您自己的通知添加到通知历史记录中。

Primetime播放器通知系统的核心是 `Notification` 类，表示独立通知。

此 `NotificationHistory` 类提供了用于收集通知的机制。 它存储表示通知集合的通知(NotificationHistoryItem)对象的日志。

要接收通知，请执行以下操作：

* 监听通知
* 将通知添加到通知历史记录

1. 监听状态更改。
1. 实施 `MediaPlayer.PlaybackEventListener.onStateChanged` 回调。
1. TVSDK向回调传递两个参数：

   * 新状态( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 对象

