---
description: MediaPlayerNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误也会导致播放器的状态发生变化。
seo-description: MediaPlayerNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误也会导致播放器的状态发生变化。
seo-title: 播放器状态、活动、错误和记录的通知
title: 播放器状态、活动、错误和记录的通知
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概述 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误也会导致播放器的状态发生变化。

应用程序可以检索通知和状态信息。 您还可以使用通知信息创建用于诊断和验证的日志记录系统。

您实现事件监听器以捕获事件并对其做出响应。 许多活动都提 `MediaPlayerNotification` 供状态通知。