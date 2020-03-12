---
description: MediaPlayerNotification对象提供有关播放器状态、警告和错误中的更改的信息。 停止播放视频的错误也会导致播放器的状态发生更改。
seo-description: MediaPlayerNotification对象提供有关播放器状态、警告和错误中的更改的信息。 停止播放视频的错误也会导致播放器的状态发生更改。
seo-title: 通知内容
title: 通知内容
uuid: 89fb8f63-b0d5-45cd-bdad-348529fd07d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 通知内容 {#notification-content}

MediaPlayerNotification对象提供有关播放器状态、警告和错误中的更改的信息。 停止播放视频的错误也会导致播放器的状态发生更改。

应用程序可以检索通知和状态信息。 您还可以使用通知信息创建用于诊断和验证的日志记录系统。

您实现事件监听器以捕获事件并对其做出响应。 许多活动都提 `MediaPlayerNotification` 供状态通知。

`MediaPlayerNotification` 提供与播放器状态相关的信息。

TVSDK提供通知的时间顺序 `MediaPlayerNotification` 列表。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * `type`:信息、警告或错误。
   * `code`:通知的数字表示。
   * `name`:通知的可读描述，如SEEK_ERROR
   * `metadata`:包含有关通知的相关信息的键／值对。 例如，名为的键 `URL` 提供一个值，该值是与通知相关的URL。

   * `innerNotification`:对直接影响此通 `MediaPlayerNotification` 知的其他对象的引用。

您可以将此信息存储在本地以供以后分析，或将其发送到远程服务器进行记录和图形表示。

## 设置通知系统 {#set-up-your-notification-system}

您可以侦听通知，也可以向通知历史记录添加您自己的通知。

Primetime Player通知系统的核心是类， `Notification` 它表示独立通知。

类提 `NotificationHistory` 供了累积通知的机制。 它存储表示通知集合的通知日志(NotificationHistoryItem)对象。

接收通知：

* 侦听通知
* 向通知历史记录添加通知

1. 侦听状态更改。
1. 实现回 `MediaPlayer.PlaybackEventListener.onStateChanged` 调。
1. TVSDK将两个参数传递给回调：

   * 新状态( `MediaPlayer.PlayerState`)
   * 对 `MediaPlayerNotification` 象

## 添加实时记录和调试 {#add-real-time-logging-and-debugging}

您可以使用通知在视频应用程序中实现实时记录。

通知系统允许您收集日志和调试信息以进行诊断和验证，而不会给系统造成过大压力。

>[!IMPORTANT]
>
>日志记录后端不是生产设置的一部分，并且不应处理高负载流量。 如果您的实施不需要完全完成，请考虑数据传输的效率，以避免系统过载。

以下是如何检索通知的示例。

1. 为视频应用程序创建基于定时器的执行线程，该线程会定期查询TVSDK通知系统收集的数据。

1. 如果计时器的间隔过大，而事件列表的大小过小，则通知事件列表将溢出。 要避免此溢出，请执行下列操作之一：

   * 减少驱动轮询新事件的线程的时间间隔。
   * 增加通知列表的大小。

1. 以JSON格式序列化最新通知事件条目，并将这些条目发送到远程服务器进行后处理。

   然后，远程服务器可以以图形方式实时显示提供的数据。
1. 要检测通知事件的丢失，请在事件索引值序列中查找间隙。

   每个通知事件都有一个索引值，该索引值由类自动递增 `session.NotificationHistory` 。

## ID3标记 {#id-tags}

ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可以在音频(AAC)和视频(H.264)流中识别ID3元数据（版本2.3.0或2.4.0），并使用其任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不属于某个可识别的版本或格式的ID3标记。 未指定编码被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出一条通知，其中包含以下数据：

* InfoCode = 303007
* 类型= ID3
* 名称=不存在
* ID = 0

1. 为实现事件监听器， `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 并向对象注册该事 `MediaPlayer` 件监听器。

   TVSDK在检测到ID3元数据时调用此监听器。

   >[!NOTE]
   >
   >自定义广告提示使用相 `onTimedMetadata` 同的事件指示检测新标记。 这不应造成任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关详细信息，请参阅custom-tags-configure。

1. 检索元数据。

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
