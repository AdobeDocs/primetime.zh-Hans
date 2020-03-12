---
description: 默认情况下，在开始播放时，VOD媒体从0开始，而实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。
seo-description: 默认情况下，在开始播放时，VOD媒体从0开始，而实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。
seo-title: 在特定时间输入流
title: 在特定时间输入流
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 在特定时间输入流 {#enter-a-stream-at-a-specific-time}

默认情况下，在开始播放时，VOD媒体从0开始，而实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。

1. 将位置传递给 `MediaPlayer.prepareToPlay`。

   TVSDK将给定位置视为资产的起始点，无需执行搜索操作。 如果该位置不在可搜索范围内，则TVSDK使用默认位置。 有关详细信息，请 [参阅在媒体播放器中加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)。

   例如：

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```
