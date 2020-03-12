---
description: 要接收有关清单中标记的通知，请实施相应的通知监听器。
seo-description: 要接收有关清单中标记的通知，请实施相应的通知监听器。
seo-title: 为定时元数据通知添加监听器
title: 为定时元数据通知添加监听器
uuid: b6939011-a6ff-4342-8e7c-3a0c805ee91c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 为定时元数据通知添加监听器 {#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请实施相应的通知监听器。

您可以通过侦听以下事件来监视定时元数据，这些事件会向应用程序通知相关活动：

* `PTTimedMetadataChangedNotification`:每次在分析内容时识别唯一的订阅标记时，TVSDK都会准备一个新对象并 `PTTimedMetadata` 调度此通知。

   该对象包含您订阅的标记的名称、播放中显示此标记的本地时间以及其他数据。

* `PTMediaPlayerTimeChangeNotification` :对于清单／播放列表定期刷新的实时／线性流，更新的播放列表／清单中可能会显示其他自定义标记，因此可能会向属 `TimedMetadata` 性中添加其他对 `MediaPlayerItem.timedMetadata` 象。

   此事件会在发生此情况时通知您的应用程序。

   通过以下方式之一检索定时元数据。

   * 将应用程序设置为将自身添加为通知的监听器， `PTTimedMetadataChangedNotification` 并使用获取对象 `PTTimedMetadataKey`。

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * 访问 `timedMetadataCollection` 的属性 `PTMediaPlayerItem`，该属性由迄今已通 `PTTimedMetadata` 知的所有对象组成。