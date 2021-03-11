---
description: 默认情况下，在开始播放时，VOD媒体开始为0，实时媒体开始为客户端实时点(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。
title: 在特定时间输入流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 1%

---


# 在特定时间{#enter-a-stream-at-a-specific-time}输入流

默认情况下，在开始播放时，VOD媒体开始为0，实时媒体开始为客户端实时点(MediaPlayer.LIVE_POINT)。 您可以覆盖默认行为。

1. 将位置传递到`MediaPlayer.prepareToPlay`。

   TVSDK将给定位置视为资产的起始点，无需执行搜索操作。 如果位置不在可搜索范围内，则TVSDK使用默认位置。 有关详细信息，请参阅[在媒体播放器中加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)。

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

