---
description: 您可以添加TVSDK行为以暂停和播放按钮。
title: 播放和暂停视频
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 播放和暂停视频{#play-and-pause-a-video}

您可以添加TVSDK行为以暂停和播放按钮。

1. 创建可执行以下操作的暂停/播放按钮。
   1. 等待您的播放器至少处于“已准备”状态。
   1. 要开始播放，请调用TVSDK play方法：

      ```
      function play():void;
      ```

   1. 要暂停播放，请调用TVSDK暂停方法：

      ```
      function pause():void;
      ```

1. 对使用回调 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 事件，以检查错误或执行其他适当的操作。

   在调用pause或play方法时，TVSDK将调用此回调。 TVSDK传递有关回调中状态更改的信息，包括新状态，如“已暂停”或“正在播放”。
