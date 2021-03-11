---
description: 您可以添加暂停和播放按钮以暂停或播放视频。
title: 播放和暂停视频
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加暂停和播放按钮以暂停或播放视频。

1. 要创建暂停或播放按钮，请执行以下操作：
   1. 等待播放器至少处于准备状态。
   1. 要播放开始，请调用`play`方法：

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 要暂停播放，请调用`pause()`方法：

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 使用状态更改的事件回调检查错误或执行其他相应操作。

   TVSDK为`pause()`或`play()`调用此回调，并传递有关状态更改的信息，包括新状态，如暂停或播放。