---
description: TVSDK处理实时视频流中的封锁，并在封锁期期间提供替代内容。
seo-description: TVSDK处理实时视频流中的封锁，并在封锁期期间提供替代内容。
seo-title: 处理实时流中的封锁
title: 处理实时流中的封锁
uuid: 1f70a272-bc77-4d41-a999-b076cb42ac5e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# 处理实时流中的封锁{#handle-blackouts-in-live-streams}

TVSDK处理实时视频流中的封锁，并在封锁期期间提供替代内容。

与编程封锁相关的最常见的用例是您的播放器应用程序向无权观看主流的用户提供替代内容。 此应用程序可使用TVSDK确定封锁期的开始和结束。 这样，在封锁期开始时，回放可以从主流切换到备用流，然后在封锁期结束时切换回主流。

要为此用例实施解决方案，请执行以下操作：

1. 设置应用程序以订阅实时流清单中的封锁标记。

   TVSDK并不直接识别封锁标记，但它允许应用程序在清单文件解析期间遇到特定标记时订阅通知。
1. 为`PTTimedMetadataChangedNotification`添加通知监听器。

   每次在清单中分析订阅标记时都会调度此通知，并从它准备新的`PTTimedMetadata`。

1. 为前景中的`PTTimedMetadata`对象实现监听器方法，如`onMediaPlayerSubscribedTagIdentified`。

1. 每次播放期间有更新时，请使用`PTMediaPlayerTimeChangeNotification`监听器处理`PTTimedMetadata`对象。

1. 添加`PTTimedMetadata`处理函数。

   此处理函数允许您切换到替代内容并返回主内容，如`PTTimedMetadata`对象及其播放时间所示。

1. 使用`onSubscribedTagInBackground`在后台为`PTTimedMetadata`对象实现监听器方法。

   此方法监视背景流的时间，帮助您确定何时可以从替代内容切换回主内容。

1. 实现背景错误的监听器方法。
1. 如果播放流的DVR中存在封锁范围，请更新不可搜索的范围。

   在以下情况下，您的应用程序必须在DVR中设置不可搜索的范围：

   * 在DVR中出现封锁时加入主流时。
   * 从备用内容切换回主内容时。

