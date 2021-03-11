---
description: MediaPlayerNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误还会导致播放器的状态发生变化。
title: 播放器状态、活动、错误和日志的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 概述{#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误还会导致播放器的状态发生变化。

应用程序可以检索通知和状态信息。 您还可以使用通知信息为诊断和验证创建日志记录系统。

您实现事件监听器以捕获和响应事件。 许多事件提供`MediaPlayerNotification`状态通知。