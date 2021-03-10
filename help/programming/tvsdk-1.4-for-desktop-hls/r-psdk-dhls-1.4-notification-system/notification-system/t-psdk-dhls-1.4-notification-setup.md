---
description: 您可以侦听通知，也可以将自己的通知添加到通知历史记录。
title: 设置通知系统
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 设置通知系统{#set-up-your-notification-system}

您可以侦听通知，也可以将自己的通知添加到通知历史记录。

Primetime Player通知系统的核心是Notification类，它表示独立通知。

NotificationHistory类提供了累积通知的机制。 它存储表示通知集合的通知(`NotificationHistoryItem`)对象日志。

要接收通知，请执行以下操作：

* 侦听通知
* 向通知历史记录添加通知

1. 侦听状态更改。
1. 实现`MediaPlayer.StatusChangeEvent.STATUS_CHANGED`事件侦听器。
1. TVSDK将`MediaPlayer.StatusChangeEvent`实例传递给事件侦听器，该侦听器包含两个参数：

   * 新状态(`MediaPlayer.Status`)
   * `MediaPlayerNotification`对象

