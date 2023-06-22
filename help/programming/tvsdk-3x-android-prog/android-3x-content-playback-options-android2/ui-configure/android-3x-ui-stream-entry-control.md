---
description: 默认情况下，开始播放时，VOD媒体从0开始，实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。
title: 在特定时间输入流
exl-id: 98688357-8394-4b62-b117-3ae2c5b0fecb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 在特定时间输入流 {#enter-a-stream-at-a-specific-time}

默认情况下，开始播放时，VOD媒体从0开始，实时媒体从客户端实时点(MediaPlayer.LIVE_POINT)开始。 您可以覆盖默认行为。

1. 将职位传递到 `MediaPlayer.prepareToPlay`.

   TVSDK将给定位置视为资源的起点，无需搜寻操作。 如果位置不在可搜索范围内，则TVSDK使用默认位置。 有关更多信息，请参阅 [在媒体播放器中加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

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
