---
description: 您可以添加TVSDK行为以暂停和播放按钮。
seo-description: 您可以添加TVSDK行为以暂停和播放按钮。
seo-title: 播放和暂停视频
title: 播放和暂停视频
uuid: 04b3b23f-5ef1-4cc4-a22f-f6ffa9cefce5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加TVSDK行为以暂停和播放按钮。

1. 创建执行以下操作的暂停／播放按钮。
   1. 等待您的播放器至少处于PREPARED状态。
   1. 要开始播放，请调用TVSDK播放方法：

      ```
      function play():void;
      ```

   1. 要暂停播放，请调用TVSDK暂停方法：

      ```
      function pause():void;
      ```

1. 使用事件回调 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 检查错误或执行其他相应的操作。

   调用pause或play方法时，TVSDK将调用此回调。 TVSDK传递有关回调中状态更改的信息，包括新状态，如PAUSED或PLAYING。
