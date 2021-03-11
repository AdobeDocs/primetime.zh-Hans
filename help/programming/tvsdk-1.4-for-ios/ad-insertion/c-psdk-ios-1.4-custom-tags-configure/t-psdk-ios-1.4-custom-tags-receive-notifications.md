---
description: 要接收有关清单中标记的通知，请实施相应的通知侦听器。
title: 为定时元数据通知添加侦听器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 为定时元数据通知{#add-listeners-for-timed-metadata-notifications}添加侦听器

要接收有关清单中标记的通知，请实施相应的通知侦听器。

您可以通过侦听以下事件来监视计时元数据，这些活动会向您的应用程序通知相关的元数据：

* `PTTimedMetadataChangedNotification`:每次在分析内容时识别唯一的订阅标记时，TVSDK会准备一个新对象并 `PTTimedMetadata` 调度此通知。

   该对象包含您订阅的标记的名称、播放中显示此标记的本地时间以及其他数据。

* `PTMediaPlayerTimeChangeNotification` :对于清单/播放列表定期刷新的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此可 `TimedMetadata` 能会向属性添加其他 `MediaPlayerItem.timedMetadata` 对象。

   此事件会在发生此情况时通知您的应用程序。

   通过以下方式之一检索定时元数据。

   * 将应用程序设置为将自身作为侦听器添加到`PTTimedMetadataChangedNotification`通知中，并使用`PTTimedMetadataKey`获取对象。

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * 访问`PTMediaPlayerItem`的`timedMetadataCollection`属性，该属性包含迄今已通知的所有`PTTimedMetadata`对象。

