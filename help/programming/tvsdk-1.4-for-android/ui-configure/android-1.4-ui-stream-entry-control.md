---
description: 默认情况下，开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。
title: 在特定时间输入流
exl-id: a16b6281-37d5-491c-a2d0-2090894c8a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 在特定时间输入流 {#enter-a-stream-at-a-specific-time}

默认情况下，开始播放时，VOD媒体从0开始(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。

1. 将职位传递到 `MediaPlayer.prepareToPlay`.

   TVSDK将给定位置视为资源的起点。 不需要搜寻操作。 如果位置不在可搜索范围内，则TVSDK使用默认位置。

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
