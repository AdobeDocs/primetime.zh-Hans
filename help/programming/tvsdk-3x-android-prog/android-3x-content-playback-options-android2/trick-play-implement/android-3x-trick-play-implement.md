---
description: 当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，请将MediaPlayer播放速率设置为1以外的值。
title: 实施快速前进和倒带
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 概述 {#implement-fast-forward-and-rewind}

当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，请将MediaPlayer播放速率设置为1以外的值。

要切换速度，必须设置一个值。

1. 通过设置播放速率，从正常播放模式(1x)切换到特技播放模式。 `MediaPlayer` 到允许的值。

       请记住以下信息：
   
   * 此 `MediaPlayerItem` 类定义允许的播放速率。
   * 如果不允许使用指定的速率，则TVSDK会选择允许的最接近的速率。

     以下示例将播放器的内部播放速率设置为请求的速率：

     ```
     import com.adobe.mediacore.MediaPlayer; 
     import com.adobe.mediacore.MediaPlayerItem; 
     import com.adobe.mediacore.MediaPlayerException; 
     import java.util.List; 
     import java.lang.Float; 
     
     private boolean setPlaybackRate(MediaPlayer player, float rate)  
       throws MediaPlayerException { 
         // Get list of playback rates that the media player supports 
         MediaPlayerItem item = player.getCurrentItem(); 
         if (item == null) return false; 
         List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
     
         // Return false if requested rate is not supported 
         if (availableRates.indexOf(rate) == -1) return false; 
     
         // Otherwise set the playback rate to the requested rate  
         // (this can throw MediaPlayerException) 
         player.setRate(rate); 
         return true; 
     }
     ```

1. 您可以选择监听速率更改事件，这会在您请求更改速率和实际发生速率更改时通知您。

TVSDK调度以下与特技播放相关的事件：

* `MediaPlayerEvent.RATE_SELECTED`，当 `rate` 值将更改为其他值。

* `MediaPlayerEvent.RATE_PLAYING`，以选定的速率继续播放时。

  当播放器从特技播放模式返回到正常播放模式时，TVSDK将调度这些事件。
