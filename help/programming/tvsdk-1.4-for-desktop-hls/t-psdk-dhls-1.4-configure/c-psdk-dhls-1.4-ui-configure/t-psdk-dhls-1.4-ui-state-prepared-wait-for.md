---
description: 在您可以使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
title: 等待有效状态
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 等待有效状态{#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK在播放器实例上提供可用于配置播放器用户界面的方法和属性。在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

播放器会在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不至少处于所需状态，则许多播放器方法会抛出`IllegalStateException`。

所需的状态通常为PREPARED。

1. 要确认状态为“已准备”，请执行以下操作：

   播放器初始化时，请等待TVSDK调用具有PREPARED状态的`MediaPlayerStatusChangeEvent.STATUS_CHANGED`事件的回调。

   检查`MediaPlayer`对象的当前状态是否至少为PREPARED。

   ```
   function getstatus():String;
   ```
