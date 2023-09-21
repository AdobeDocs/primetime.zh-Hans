---
description: TVSDK可处理实时视频流中的中断，并在中断期间提供替代内容。
title: 处理封锁
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 处理封锁 {#handle-blackouts}

TVSDK可处理实时视频流中的中断，并在中断期间提供替代内容。

与编程中断相关的最常见用例是，当播放器应用程序向无权观看主流的用户提供替代内容时。 此应用程序可以使用TVSDK确定封锁期的开始和结束。 这样，在中断期开始时，播放可以从主流切换到备用流，然后在中断期结束时切换回主流。

要实施此用例的解决方案，请执行以下操作：

1. 设置应用程序以订阅实时流清单中的封锁标记。

   TVSDK不会直接感知封锁标记，但它允许您的应用程序在解析清单文件期间遇到特定标记时订阅通知。
1. 添加通知侦听器 `PTTimedMetadataChangedNotification`.

   每次在清单中解析订阅的标记时，都会发送此通知，并且会发送新的 `PTTimedMetadata` 是由它制成的。

1. 实施监听程序方法，例如 `onMediaPlayerSubscribedTagIdentified`，用于 `PTTimedMetadata` 前景中的对象。

1. 每次在播放期间进行更新时，请使用 `PTMediaPlayerTimeChangeNotification` 要处理的侦听器 `PTTimedMetadata` 对象。

1. 添加 `PTTimedMetadata` 处理程序。

   此处理程序允许您切换到替代内容并返回主内容，如 `PTTimedMetadata` 对象及其播放时间。

1. 使用 `onSubscribedTagInBackground` 为实施监听程序方法 `PTTimedMetadata` 背景中的对象。

   此方法监控后台流上的时间，这有助于您确定何时可以从替代内容切换回主内容。

1. 为后台错误实施侦听程序方法。
1. 如果封锁范围位于播放流的DVR中，请更新不可搜索的范围。

   在以下情况下，您的应用程序必须在DVR中设置不可搜索范围：

   * 当DVR中存在中断时加入主流。
   * 从替换内容切换回主内容时。
