---
description: 默认情况下，开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。
title: 在特定时间输入流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 在特定时间输入流 {#enter-a-stream-at-a-specific-time}

默认情况下，开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。

1. 将职位传递给 `MediaPlayer.prepareToPlay`.

   TVSDK将给定位置视为资源的起点。 不需要搜寻操作。 如果该位置不在可搜索范围内，则TVSDK将使用默认位置。

   例如：

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   ```
