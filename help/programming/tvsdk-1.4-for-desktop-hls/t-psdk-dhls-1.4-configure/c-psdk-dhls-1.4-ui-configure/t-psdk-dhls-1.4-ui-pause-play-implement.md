---
description: 您可以添加TVSDK行为以暂停和播放按钮。
title: 播放和暂停视频
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 播放和暂停视频{#play-and-pause-a-video}

您可以添加TVSDK行为以暂停和播放按钮。

1. 创建执行以下操作的暂停/播放按钮。
   1. 等待播放器至少处于PREPARED状态。
   1. 要播放开始，请调用TVSDK播放方法：

      ```
      function play():void;
      ```

   1. 要暂停播放，请调用TVSDK暂停方法：

      ```
      function pause():void;
      ```

1. 使用`MediaPlayerStatusChangeEvent.STATUS_CHANGED`事件的回调检查错误或执行其他相应操作。

   调用pause或play方法时，TVSDK将调用此回调。 TVSDK传递有关回调中状态更改的信息，包括新状态，如PAUSED或PLAYING。
