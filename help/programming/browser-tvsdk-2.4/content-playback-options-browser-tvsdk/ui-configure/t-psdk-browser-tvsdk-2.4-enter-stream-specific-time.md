---
description: 默认情况下，当播放开始时，VOD媒体从0开始，实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。
title: 在特定时间输入流
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 在特定时间输入流{#enter-a-stream-at-a-specific-time}

默认情况下，当播放开始时，VOD媒体从0开始，实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。

1. 将职位传递到 `MediaPlayer.prepareToPlay`.
1. 浏览器TVSDK将此位置用作资源的起点。

   >[!NOTE]
   >
   >不需要搜寻操作。

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
