---
description: MediaPlayerStatus对象提供有关播放器状态更改的信息。 通知对象提供有关警告和错误的信息。 停止播放视频的错误也会导致播放器状态发生变化。 您可以实施事件侦听器来捕获和响应事件（MediaPlayerEvent对象）。
title: 播放器状态、活动、错误和日志记录的通知和事件
exl-id: c25e834e-ffa0-444c-9285-331e6841ac29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 播放器状态、活动、错误和日志记录的通知和事件 {#notifications-and-events-for-player-status-activity-errors-and-logging}

事件和通知可帮助您管理视频应用程序的异步方面。

MediaPlayerStatus对象提供有关播放器状态更改的信息。 通知对象提供有关警告和错误的信息。 停止播放视频的错误也会导致播放器状态发生变化。 您可以实施事件侦听器来捕获和响应事件（MediaPlayerEvent对象）。

您的应用程序可以检索通知和状态信息。 使用此信息，您还可以创建用于诊断和验证的日志记录系统。

## 通知内容 {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` 提供与播放器状态相关的信息。

TVSDK提供了按时间顺序排列的 `MediaPlayerNotification` 通知，每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * `type`：信息、警告或错误。
   * `code`：通知的数值表示形式。
   * `name`：人类可读的通知描述，如SEEK_ERROR
   * `metadata`：包含有关通知的相关信息的键/值对。 例如，一个名为的键 `URL` 提供一个值，该值为与通知相关的URL。

   * `innerNotification`：对另一个的引用 `MediaPlayerNotification` 直接影响此通知的对象。

您可以将此信息存储在本地，以供以后分析使用，也可以将其发送到远程服务器以进行日志记录和图形显示。

## 设置通知系统 {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

您可以监听通知。

Primetime播放器通知系统的核心是 `Notification` 类，表示独立通知。

要接收通知，请监听如下通知：

1. 实施 `NotificationEventListener.onNotification()` 回调。
1. TVSDK传递 `NotificationEvent` 对象。

   >[!NOTE]
   >
   >通知类型列于 `Notification.Type` 枚举：

   * `ERROR`
   * `INFO`
   * `WARNING`

## 添加实时日志记录和调试 {#section_9D4004308CB243AD9B50818895D10005}

您可以使用通知在视频应用程序中实施实时日志记录。

通知系统允许您收集日志记录和调试信息以进行诊断和验证，而不会给系统带来压力。

>[!IMPORTANT]
>
>日志记录后端不是生产设置的一部分，不应处理高负载流量。 如果您的实施不需要完全完成，请考虑数据传输的效率，以避免系统过载。

以下是如何检索通知的示例：

1. 为您的视频应用程序创建一个基于计时器的执行线程，定期查询TVSDK通知系统收集的数据。
1. 如果计时器的间隔太大，而事件列表的大小太小，则通知事件列表将溢出。

   >[!NOTE]
   >
   >要避免此溢出，请执行以下操作之一：
   >
   >1. 缩短驱动轮询新事件的线程的时间间隔。
   >1. 增加通知列表的大小。


1. 以JSON格式序列化最新的通知事件条目，并将这些条目发送到远程服务器进行后处理。

   >[!NOTE]
   >
   >远程服务器可以实时地以图形方式显示提供的数据。

1. 要检测通知事件丢失，请查找事件索引值序列中的间隔。
