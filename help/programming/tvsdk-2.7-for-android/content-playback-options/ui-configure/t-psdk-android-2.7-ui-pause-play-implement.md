---
description: 您可以添加暂停和播放按钮以暂停或播放视频。
seo-description: 您可以添加暂停和播放按钮以暂停或播放视频。
seo-title: 播放和暂停视频
title: 播放和暂停视频
uuid: 66fefead-7f1d-46ed-a23e-381f25697978
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加暂停和播放按钮以暂停或播放视频。

1. 创建暂停或播放按钮：
   1. 等待玩家至少处于准备状态。
   1. 要开始播放，请调用`play`方法：

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 要暂停播放，请调用`pause()`方法：

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 使用状态更改的事件回调检查错误或执行其他适当的操作。

   TVSDK为`pause()`或`play()`调用此回调，并传递有关状态更改的信息，包括新状态，如暂停或播放。

