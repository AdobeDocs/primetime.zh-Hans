---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
title: 等待有效的状态
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 等待有效的状态 {#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK提供播放器实例上的方法和属性，可用于配置播放器用户界面。在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

播放器会通过各种状态进行移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器未至少处于所需的状态，则许多播放器方法会引发 `IllegalStateException`.

所需的状态通常为PREPARED。

1. 要确认状态为“已准备”，请执行以下操作：

   当播放器初始化时，等待TVSDK调用的 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有PREPARED状态的事件。

   要检查的当前 `MediaPlayer` 对象至少为PREPARED。

   ```
   function getstatus():String;
   ```
