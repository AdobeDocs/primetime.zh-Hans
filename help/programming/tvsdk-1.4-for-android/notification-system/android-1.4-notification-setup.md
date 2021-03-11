---
description: 您可以侦听通知，也可以将自己的通知添加到通知历史记录。
title: 设置通知系统
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 设置通知系统{#set-up-your-notification-system}

您可以侦听通知，也可以将自己的通知添加到通知历史记录。

Primetime Player通知系统的核心是`Notification`类，它表示独立通知。

`NotificationHistory`类提供了累积通知的机制。 它存储表示通知集合的通知日志(NotificationHistoryItem)对象。

要接收通知，请执行以下操作：

* 侦听通知
* 向通知历史记录添加通知

1. 侦听状态更改。
1. 实现`MediaPlayer.PlaybackEventListener.onStateChanged`回调。
1. TVSDK将两个参数传递给回调：

   * 新状态(`MediaPlayer.PlayerState`)
   * `MediaPlayerNotification`对象

