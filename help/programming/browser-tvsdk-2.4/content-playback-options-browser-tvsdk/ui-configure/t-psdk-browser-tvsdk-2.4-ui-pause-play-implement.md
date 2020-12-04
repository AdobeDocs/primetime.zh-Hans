---
description: 您可以添加浏览器TVSDK行为以暂停和播放按钮。
seo-description: 您可以添加浏览器TVSDK行为以暂停和播放按钮。
seo-title: 播放和暂停视频
title: 播放和暂停视频
uuid: 4053ea9e-6b74-41e9-ad04-087ad13e3698
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加浏览器TVSDK行为以暂停和播放按钮。

1. 创建执行以下操作的暂停／播放按钮。
   1. 等待您的播放器至少处于PREPARED状态。
   1. 要播放开始，请调用浏览器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 要暂停播放，请调用浏览器TVSDK暂停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 侦听`AdobePSDK.MediaPlayerStatusChangeEvent`事件检查错误或执行其他适当操作。

   当调用暂停或播放方法时，浏览器TVSDK会触发此事件，并传递有关事件对象的信息，包括新状态，如`MediaPlayerStatus.PLAYING`或`MediaPlayerStatus.PAUSED`。

