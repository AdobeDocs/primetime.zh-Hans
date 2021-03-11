---
description: TVSDK处理实时视频流中的封锁，并在封锁期间提供替代内容。
title: 处理封锁
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# 处理封锁{#handle-blackouts}

TVSDK处理实时视频流中的封锁，并在封锁期间提供替代内容。

与编程封锁相关的最常见用例是，您的播放器应用程序向没有资格观看主流的用户提供替代内容。 此应用程序可使用TVSDK确定封锁期的开始和结束。 这样，在封锁期开始时，回放可以从主流切换到备用流，然后在封锁期结束时切换回主流。

要为此用例实施解决方案，请执行以下操作：

1. 设置应用程序以订阅实时流清单中的封锁标记。

   TVSDK并不直接知道封锁标记，但它允许应用程序在清单文件解析期间遇到特定标记时订阅通知。
1. 为`PTTimedMetadataChangedNotification`添加通知侦听器。

   每次在清单中分析订阅标记并从中准备新的`PTTimedMetadata`时都会调度此通知。

1. 对前景中的`PTTimedMetadata`对象实现监听器方法，如`onMediaPlayerSubscribedTagIdentified`。

1. 每次播放期间出现更新时，使用`PTMediaPlayerTimeChangeNotification`侦听器处理`PTTimedMetadata`对象。

1. 添加`PTTimedMetadata`处理函数。

   此处理函数允许您切换到替代内容，并返回到由`PTTimedMetadata`对象及其播放时间指示的主内容。

1. 使用`onSubscribedTagInBackground`为后台中的`PTTimedMetadata`对象实现监听器方法。

   此方法监视后台流的计时，这有助于您确定何时可以从替代内容切换回主内容。

1. 为背景错误实现侦听器方法。
1. 如果封锁范围在播放流的DVR中，请更新不可查看的范围。

   在以下情况下，您的应用程序必须在DVR中设置不可搜索的范围：

   * 在DVR中出现封锁时加入主流时。
   * 从替代内容切换回主内容时。