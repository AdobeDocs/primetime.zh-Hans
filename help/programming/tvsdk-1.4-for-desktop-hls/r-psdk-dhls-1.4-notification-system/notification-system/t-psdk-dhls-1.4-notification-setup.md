---
description: 您可以侦听通知，也可以向通知历史记录添加您自己的通知。
seo-description: 您可以侦听通知，也可以向通知历史记录添加您自己的通知。
seo-title: 设置通知系统
title: 设置通知系统
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 设置通知系统{#set-up-your-notification-system}

您可以侦听通知，也可以向通知历史记录添加您自己的通知。

Primetime Player通知系统的核心是Notification类，它表示独立通知。

NotificationHistory类提供了累积通知的机制。 它存储表示通知集合 `NotificationHistoryItem`的通知()对象日志。

接收通知：

* 侦听通知
* 向通知历史记录添加通知

1. 侦听状态更改。
1. 实现事 `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` 件监听器。
1. TVSDK将一个实 `MediaPlayer.StatusChangeEvent` 例传递给事件监听器，它包含两个参数：

   * 新状态( `MediaPlayer.Status`)
   * 对 `MediaPlayerNotification` 象

