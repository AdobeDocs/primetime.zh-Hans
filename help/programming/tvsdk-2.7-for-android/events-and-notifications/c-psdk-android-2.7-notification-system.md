---
description: MediaPlayerStatus对象提供有关播放器状态更改的信息。 通知对象提供有关警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。 您实现事件监听器以捕获事件（MediaPlayerEvent对象）并对其做出响应。
seo-description: MediaPlayerStatus对象提供有关播放器状态更改的信息。 通知对象提供有关警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。 您实现事件监听器以捕获事件（MediaPlayerEvent对象）并对其做出响应。
seo-title: 播放器状态、活动、错误和记录的通知和事件
title: 播放器状态、活动、错误和记录的通知和事件
uuid: ec840f14-38d1-4f43-b119-e1326515fc63
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# 播放器状态、活动、错误和记录的通知和事件 {#notifications-and-events-for-player-status-activity-errors-and-logging}

事件和通知可帮助您管理视频应用程序的异步方面。

MediaPlayerStatus对象提供有关播放器状态更改的信息。 通知对象提供有关警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。 您实现事件监听器以捕获事件（MediaPlayerEvent对象）并对其做出响应。

应用程序可以检索通知和状态信息。 使用此信息，您还可以创建用于诊断和验证的日志记录系统。

## 通知内容 {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` 提供与播放器状态相关的信息。

TVSDK提供按时间顺序排 `MediaPlayerNotification` 列的通知列表，每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * `type`:信息、警告或错误。
   * `code`:通知的数字表示。
   * `name`:通知的可读描述，如SEEK_ERROR
   * `metadata`:包含有关通知的相关信息的键／值对。 例如，名为的键 `URL` 提供一个值，该值是与通知相关的URL。

   * `innerNotification`:直接影响此 `MediaPlayerNotification` 通知的对象的引用。

您可以将此信息存储在本地以供以后分析，或将其发送到远程服务器以进行记录和图形表示。

## 设置通知系统 {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

您可以监听通知。

Primetime Player通知系统的核心是类， `Notification` 它表示独立通知。

要接收通知，请按如下方式侦听通知：

1. 实现回 `NotificationEventListener.onNotification()` 调。
1. TVSDK将对 `NotificationEvent` 象传递到回调。

   >[!NOTE]
   >
   >通知类型在枚举中 `Notification.Type` 枚举：

   * `ERROR`
   * `INFO`
   * `WARNING`

## 添加实时记录和调试 {#section_9D4004308CB243AD9B50818895D10005}

您可以使用通知在视频应用程序中实现实时记录。

通知系统允许您收集日志记录和调试信息以进行诊断和验证，而不会给系统带来压力。

>[!IMPORTANT]
>
>日志记录后端不是生产设置的一部分，不应处理高负载流量。 如果您的实施不需要完全完成，请考虑数据传输的效率，以避免系统过载。

以下是如何检索通知的示例：

1. 为视频应用程序创建一个基于定时器的执行线程，定期查询TVSDK通知系统收集的数据。
1. 如果计时器的间隔过大，且事件列表的大小过小，则通知事件列表将溢出。

   >[!NOTE]
   >
   >要避免此溢出，请执行下列操作之一：
   >
   >1. 减少驱动轮询新事件的线程的时间间隔。
   >1. 增加通知列表的大小。


1. 以JSON格式序列化最新通知事件条目，并将这些条目发送到远程服务器进行后处理。

   >[!NOTE]
   >
   >远程服务器可以以图形方式实时显示所提供的数据。

1. 要检测通知事件丢失，请在事件索引值序列中查找间隙。

