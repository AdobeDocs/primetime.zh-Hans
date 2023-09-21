---
description: 您可以监听通知，也可以将您自己的通知添加到通知历史记录中。
title: 设置通知系统
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 设置通知系统{#set-up-your-notification-system}

您可以监听通知，也可以将您自己的通知添加到通知历史记录中。

Primetime播放器通知系统的核心是Notification类，它表示独立通知。

NotificationHistory类提供了用于累积通知的机制。 它存储通知日志( `NotificationHistoryItem`)对象，表示通知集合。

要接收通知，请执行以下操作：

* 收听通知
* 将通知添加到通知历史记录

1. 监听状态更改。
1. 实施 `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` 事件侦听器。
1. TVSDK传递 `MediaPlayer.StatusChangeEvent` 事件侦听器的实例，其中包含两个参数：

   * 新状态( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` 对象
