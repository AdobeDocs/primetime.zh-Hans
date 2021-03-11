---
description: 您可以添加浏览器TVSDK行为以暂停和播放按钮。
title: 播放和暂停视频
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加浏览器TVSDK行为以暂停和播放按钮。

1. 创建执行以下操作的暂停/播放按钮。
   1. 等待播放器至少处于PREPARED状态。
   1. 要播放开始，请调用浏览器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 要暂停播放，请调用Browser TVSDK暂停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 侦听`AdobePSDK.MediaPlayerStatusChangeEvent`事件以检查错误或执行其他相应操作。

   当调用暂停或播放方法时，浏览器TVSDK会触发此事件，并传递有关事件对象的信息，包括新状态，如`MediaPlayerStatus.PLAYING`或`MediaPlayerStatus.PAUSED`。

