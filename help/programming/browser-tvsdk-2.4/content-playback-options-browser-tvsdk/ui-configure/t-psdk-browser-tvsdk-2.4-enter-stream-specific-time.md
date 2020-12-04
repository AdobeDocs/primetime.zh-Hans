---
description: 默认情况下，当播放开始、0的VOD媒体开始和客户端实时点(MediaPlayer.LIVE_POINT)的实时媒体开始时。 您可以覆盖默认行为。
seo-description: 默认情况下，当播放开始、0的VOD媒体开始和客户端实时点(MediaPlayer.LIVE_POINT)的实时媒体开始时。 您可以覆盖默认行为。
seo-title: 在特定时间输入流
title: 在特定时间输入流
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# 在特定时间输入流{#enter-a-stream-at-a-specific-time}

默认情况下，当播放开始、0的VOD媒体开始和客户端实时点(MediaPlayer.LIVE_POINT)的实时媒体开始时。 您可以覆盖默认行为。

1. 将位置传递到`MediaPlayer.prepareToPlay`。
1. 浏览器TVSDK使用此位置作为资产的起点。

   >[!NOTE]
   >
   >无需执行搜索操作。

1. 如果位置不在可搜索范围内，则使用默认位置。

   例如：

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

