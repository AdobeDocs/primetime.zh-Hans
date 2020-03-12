---
description: 默认情况下，在开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。
seo-description: 默认情况下，在开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。
seo-title: 在特定时间输入流
title: 在特定时间输入流
uuid: ac3479e2-46a1-4ac8-a9e8-68a23f5dd74d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在特定时间输入流 {#enter-a-stream-at-a-specific-time}

默认情况下，在开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。

1. 将位置传递给 `MediaPlayer.prepareToPlay`。

   TVSDK将给定位置视为资产的起始点。 无需执行搜索操作。 如果该位置不在可搜索范围内，则TVSDK使用默认位置。

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

