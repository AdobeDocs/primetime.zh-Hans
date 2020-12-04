---
description: 您可以添加TVSDK行为以暂停和播放按钮。
seo-description: 您可以添加TVSDK行为以暂停和播放按钮。
seo-title: 播放和暂停视频
title: 播放和暂停视频
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加TVSDK行为以暂停和播放按钮。

1. 创建执行以下操作的暂停／播放按钮。
   1. 等待您的播放器至少处于PREPARED状态。
   1. 要播放开始，请调用TVSDK播放方法：

      ```java
      void play() throws IllegalStateException;
      ```

   1. 要暂停播放，请调用TVSDK暂停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 使用`MediaPlayer.PlaybackEventListener.onStateChanged`回调检查错误或执行其他适当的操作。

   调用暂停或播放方法时，TVSDK将调用此回调。 TVSDK传递有关回调中状态更改的信息，包括新状态，如PAUSED或PLAYING。

