---
description: 在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。
title: 等待有效的状态
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 等待有效的状态 {#wait-for-a-valid-state}

通过TVSDK，您可以控制实时和视频点播(VOD)的基本播放体验。 TVSDK提供了播放器实例上的方法和属性，可用于配置播放器用户界面。在使用大多数TVSDK播放器方法之前，播放器必须处于有效状态。

播放器会经历各种状态。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器未至少处于所需的状态，则许多播放器方法会引发 `IllegalStateException`.

所需的状态通常为PREPARED。

1. 要确认状态为PREPARED，请执行以下操作：

   当播放器初始化时，等待TVSDK为调用回调 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有PREPARED状态的事件。

   检查的当前 `MediaPlayer` 对象至少为PREPARED。

   ```
   function getstatus():String;
   ```
