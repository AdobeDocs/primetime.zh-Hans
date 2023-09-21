---
description: MediaPlayerNotification对象提供有关播放器状态更改、警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。
title: 播放器状态、活动、错误和日志记录的通知
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 概述 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification对象提供有关播放器状态更改、警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。

您的应用程序可以检索通知和状态信息。 还可以使用通知信息创建用于诊断和验证的日志记录系统。

您可以实施事件侦听器来捕获和响应事件。 许多事件都提供 `MediaPlayerNotification` 状态通知。
