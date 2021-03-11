---
description: 默认情况下，当播放开始时，VOD媒体开始为0，实时媒体开始为客户端实时点(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。
title: 在特定时间输入流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# 在特定时间输入流{#enter-a-stream-at-a-specific-time}

默认情况下，当播放开始时，VOD媒体开始为0，实时媒体开始为客户端实时点(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。

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

