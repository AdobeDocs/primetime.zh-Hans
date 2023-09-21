---
description: MediaPlayerNotification对象提供有关播放器状态更改、警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。
title: 通知内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 通知内容 {#notification-content}

MediaPlayerNotification对象提供有关播放器状态更改、警告和错误的信息。 停止播放视频的错误也会导致播放器的状态发生变化。

您的应用程序可以检索通知和状态信息。 还可以使用通知信息创建用于诊断和验证的日志记录系统。

您可以实施事件侦听器来捕获和响应事件。 许多事件都提供 `MediaPlayerNotification` 状态通知。

`MediaPlayerNotification` 提供与播放器状态相关的信息。

TVSDK按时间顺序列出了以下列表： `MediaPlayerNotification` 通知。 每个通知都包含以下信息：

* 时间戳
* 诊断元数据包含以下元素：

   * `type`：信息、警告或错误。
   * `code`：通知的数值表示形式。
   * `name`：人类可读的通知描述，如SEEK_ERROR
   * `metadata`：包含有关通知的信息的键/值对。 例如，名为的键 `URL` 提供一个值，该值为与通知相关的URL。

   * `innerNotification`：对另一个的引用 `MediaPlayerNotification` 直接影响此通知的对象。

您可以将此信息存储在本地，以供以后分析使用，也可以将其发送到远程服务器以供日志记录和图形显示。

## 设置通知系统 {#set-up-your-notification-system}

您可以监听通知，也可以将您自己的通知添加到通知历史记录中。

Primetime播放器通知系统的核心是 `Notification` 类，表示独立通知。

此 `NotificationHistory` 类提供了用于累积通知的机制。 它存储代表通知集合的通知(NotificationHistoryItem)对象的日志。

要接收通知，请执行以下操作：

* 收听通知
* 将通知添加到通知历史记录

1. 监听状态更改。
1. 实施 `MediaPlayer.PlaybackEventListener.onStateChanged` 回调。
1. TVSDK向回调传递两个参数：

   * 新状态( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 对象

## 添加实时日志记录和调试 {#add-real-time-logging-and-debugging}

您可以使用通知在视频应用程序中实施实时日志记录。

通知系统允许您收集用于诊断和验证的日志记录和调试信息，而不会对系统造成过大的压力。

>[!IMPORTANT]
>
>日志记录后端不是生产设置的一部分，不应处理高负载流量。 如果您的实施不需要完全完成，请考虑数据传输的效率，以避免系统过载。

以下是如何检索通知的示例。

1. 为视频应用程序创建一个基于计时器的执行线程，定期查询TVSDK通知系统收集的数据。

1. 如果计时器的间隔太大，而事件列表的大小太小，则通知事件列表将溢出。 要避免此溢出，请执行以下操作之一：

   * 缩短驱动轮询新事件的线程的时间间隔。
   * 增加通知列表的大小。

1. 以JSON格式序列化最新的通知事件条目，并将这些条目发送到远程服务器进行后处理。

   然后，远程服务器能够以图形方式实时显示提供的数据。
1. 要检测通知事件丢失，请查找事件索引值序列中的间隔。

   每个通知事件都有一个索引值，该值自动递增 `session.NotificationHistory` 类。

## ID3标记 {#id-tags}

ID3标记提供有关音频或视频文件的信息，例如文件标题或艺术家姓名。 TVSDK在HLS流中的传输流(TS)区段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

>[!IMPORTANT]
>
>TVSDK可将其音频(AAC)和视频(H.264)流中的ID3元数据（版本2.3.0或2.4.0）识别为任何可能的编码（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它会忽略不采用可识别版本或格式之一的ID3标记。 未指定的编码将被视为UTF8。

当TVSDK检测到ID3元数据时，它会发出包含以下数据的通知：

* 信息代码= 303007
* 类型= ID3
* 名称=不存在
* ID = 0

1. 为实施事件侦听器 `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 并在 `MediaPlayer` 对象。

   TVSDK在检测到ID3元数据时会调用此侦听器。

   >[!NOTE]
   >
   >自定义广告提示使用相同的 `onTimedMetadata` 指示检测到新标记的事件。 这应该不会导致任何混淆，因为在清单级别检测到自定义广告提示，并且ID3标记嵌入到流中。 有关更多信息，请参阅custom-tags-configure 。

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
