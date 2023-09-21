---
description: 要接收有关清单中标记的通知，请实施相应的通知侦听器。
title: 为定时元数据通知添加侦听器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 为定时元数据通知添加侦听器 {#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请实施相应的通知侦听器。

您可以通过侦听以下事件来监视定时元数据，这些事件会通知您的应用程序相关活动：

* `PTTimedMetadataChangedNotification`：在分析内容期间，每次标识唯一的订阅标记时，TVSDK都会准备一个新的 `PTTimedMetadata` 对象并调度此通知。

  对象包含您订阅的标记的名称、播放中将显示此标记的本地时间以及其他数据。

* `PTMediaPlayerTimeChangeNotification` ：对于清单/播放列表定期刷新的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此也会显示 `TimedMetadata` 对象可添加到 `MediaPlayerItem.timedMetadata` 属性。

  此事件会在发生这种情况时通知应用程序。

  通过以下方式之一检索定时元数据。

   * 将应用程序设置为将其自身作为侦听器添加到 `PTTimedMetadataChangedNotification` 通知，并使用获取对象 `PTTimedMetadataKey`.

     ```
     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
       name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
     
     - (void) onTimedMetadataChanged:(NSNotification *) notification { 
         NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
         PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
     }
     ```

   * 访问 `timedMetadataCollection` 属性 `PTMediaPlayerItem`，其中包含所有 `PTTimedMetadata` 到目前为止已通知的对象。
