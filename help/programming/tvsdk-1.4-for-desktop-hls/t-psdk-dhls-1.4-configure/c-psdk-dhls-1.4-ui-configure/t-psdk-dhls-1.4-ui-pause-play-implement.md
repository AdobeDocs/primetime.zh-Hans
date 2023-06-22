---
description: 您可以将TVSDK行为添加到暂停和播放按钮。
title: 播放和暂停视频
exl-id: c1c259a4-edb8-475b-96a2-7fa0903804c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 播放和暂停视频{#play-and-pause-a-video}

您可以将TVSDK行为添加到暂停和播放按钮。

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

1. 使用回调进行 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 事件，以检查错误或执行其他适当的操作。

   在调用pause或play方法时，TVSDK会调用此回调。 TVSDK传递有关回调中状态更改的信息，包括新状态，如“已暂停”或“正在播放”。
