---
description: 要接收有关清单中标记的通知，请实施相应的通知监听器。
seo-description: 要接收有关清单中标记的通知，请实施相应的通知监听器。
seo-title: 为定时元数据通知添加监听器
title: 为定时元数据通知添加监听器
uuid: dcd1bd92-0617-4eab-8b06-7301aaff42f3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 为定时元数据通知添加监听器{#add-listeners-for-timed-metadata-notifications}

要接收有关清单中标记的通知，请实施相应的通知监听器。

您可以通过监听以下事件来监视定时元数据，这些活动会通知您的应用程序相关的：

* `PTTimedMetadataChangedNotification`:每次在分析内容时识别唯一的订阅标记时，TVSDK会准备一个新对 `PTTimedMetadata` 象并调度此通知。

   该对象包含您订阅的标记的名称、播放中显示此标记的本地时间以及其他数据。

* `PTMediaPlayerTimeChangeNotification` :对于清单／播放列表定期刷新的实时／线性流，更新的播放列表／清单中可能显示其他自定义标记， `TimedMetadata` 因此可能会向属性添加其 `MediaPlayerItem.timedMetadata` 他对象。

   此事件会在发生此情况时通知您的应用程序。

   通过以下方式之一检索定时元数据。

   * 将应用程序设置为将自身添加为`PTTimedMetadataChangedNotification`通知的监听器，并使用`PTTimedMetadataKey`获取对象。

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * 访问`PTMediaPlayerItem`的`timedMetadataCollection`属性，该属性包含迄今已通知的所有`PTTimedMetadata`对象。

