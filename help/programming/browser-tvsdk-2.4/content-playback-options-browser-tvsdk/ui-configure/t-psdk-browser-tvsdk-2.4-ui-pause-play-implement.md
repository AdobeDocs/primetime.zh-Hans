---
description: 您可以添加浏览器TVSDK行为以暂停和播放按钮。
title: 播放和暂停视频
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放和暂停视频{#play-and-pause-a-video}

您可以添加浏览器TVSDK行为以暂停和播放按钮。

1. 创建可执行以下操作的暂停/播放按钮。
   1. 等待您的播放器至少处于“已准备”状态。
   1. 要开始播放，请调用浏览器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 要暂停播放，请调用浏览器TVSDK暂停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 聆听 `AdobePSDK.MediaPlayerStatusChangeEvent` 事件，以检查错误或执行其他适当的操作。

   在调用暂停或播放方法并传递有关事件对象的信息(包括新状态，例如 `MediaPlayerStatus.PLAYING` 或 `MediaPlayerStatus.PAUSED`.
