---
description: TVSDK处理实时视频流中的封锁期，并在封锁期间提供替代内容。
seo-description: TVSDK处理实时视频流中的封锁期，并在封锁期间提供替代内容。
seo-title: 处理封锁
title: 处理封锁
uuid: 00b6f204-6ba4-4245-9028-6f7c392e9275
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 处理封锁 {#handle-blackouts}

TVSDK处理实时视频流中的封锁期，并在封锁期间提供替代内容。

与编程封锁相关的最常见的用例是您的播放器应用程序向没有资格观看主流的用户提供替代内容。 此应用程序可使用TVSDK确定封锁期的开始和结束。 这样，在封锁期开始时，回放可以从主流切换到备用流，然后在封锁期结束时切换回主流。

要为此用例实施解决方案，请执行以下操作：

1. 设置应用程序以订阅实时流清单中的封锁标记。

   TVSDK并不直接了解封锁标记，但它允许应用程序在清单文件解析过程中遇到特定标记时订阅通知。
1. 为添加通知监听器 `PTTimedMetadataChangedNotification`。

   每次在清单中分析订阅标签并从其准备新标签时，都会调 `PTTimedMetadata` 度此通知。

1. 实现监听器方法，如 `onMediaPlayerSubscribedTagIdentified`前景中 `PTTimedMetadata` 的对象的监听器方法。

1. 每次播放期间出现更新时，都使用监 `PTMediaPlayerTimeChangeNotification` 听器处理对 `PTTimedMetadata` 象。

1. 添加处理 `PTTimedMetadata` 函数。

   此处理函数允许您切换到替代内容并返回到由对象及其播放时间指示 `PTTimedMetadata` 的主内容。

1. 使用 `onSubscribedTagInBackground` 为背景中的对象实 `PTTimedMetadata` 现监听器方法。

   此方法监视背景流的时间，这有助于您确定何时可以从替代内容切换回主内容。

1. 为背景错误实现监听器方法。
1. 如果播放流的DVR中存在封锁范围，请更新不可搜索的范围。

   在以下情况下，您的应用程序必须在DVR中设置不可搜索的范围：

   * 在DVR中封锁期时加入主流时。
   * 从替代内容切换回主内容时。