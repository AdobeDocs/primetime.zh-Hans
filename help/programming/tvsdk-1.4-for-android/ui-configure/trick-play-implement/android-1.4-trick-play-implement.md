---
description: 当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为1以外的值。
title: 实现快速前进和倒带
exl-id: 58ed9a96-9617-4364-81d4-b404b23cf265
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 概述 {#implement-fast-forward-and-rewind-overview}

当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为1以外的值。

要切换速度，必须设置一个值。

1. 通过将速率设置为从正常播放模式(1x)移动到特技播放模式 `MediaPlayer` 到允许的值。

   * 此 `MediaPlayerItem` 类定义允许的播放速率。
   * 如果不允许指定的速率，则TVSDK会选择允许的最接近的速率。

   此示例将播放器的内部播放速率设置为请求的速率。

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
   
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
   
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
   
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. 您可以选择监听速率更改事件，这可以让您知道何时请求速率更改以及何时实际发生速率更改。

       TVSDK调度以下与特技播放相关的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 当 `rate` 值会更改为其他值。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以选定的速率继续播放时。

      当播放器从特技播放模式返回到正常播放模式时，TVSDK会调度这两个事件。
