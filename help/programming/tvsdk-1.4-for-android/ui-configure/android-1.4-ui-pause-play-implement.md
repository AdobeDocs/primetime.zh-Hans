---
description: 您可以将TVSDK行为添加到暂停和播放按钮。
title: 播放和暂停视频
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放和暂停视频{#play-and-pause-a-video}

您可以将TVSDK行为添加到暂停和播放按钮。

1. 创建可执行以下操作的暂停/播放按钮。
   1. 等待您的播放器至少处于“已准备”状态。
   1. 要开始播放，请调用TVSDK play方法：

      ```java
      void play() throws IllegalStateException;
      ```

   1. 要暂停播放，请调用TVSDK暂停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 使用 `MediaPlayer.PlaybackEventListener.onStateChanged` 回调以检查错误或执行其他适当的操作。

   在调用pause或play方法时，TVSDK会调用此回调。 TVSDK传递有关回调中的状态更改的信息，包括新状态，如“已暂停”或“正在播放”。
