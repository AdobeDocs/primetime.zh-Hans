---
description: 当用户在媒体中快速前进或快速后退时，他们处于特技播放模式。 要进入特技播放模式，请将MediaPlayer播放速率设置为1以外的值。
seo-description: 当用户在媒体中快速前进或快速后退时，他们处于特技播放模式。 要进入特技播放模式，请将MediaPlayer播放速率设置为1以外的值。
seo-title: 实现快进和后退
title: 实现快进和后退
uuid: d54c8c61-887f-4362-9085-e443859854b9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 概述 {#implement-fast-forward-and-rewind}

当用户在媒体中快速前进或快速后退时，他们处于特技播放模式。 要进入特技播放模式，请将MediaPlayer播放速率设置为1以外的值。

要切换速度，必须设置一个值。

1. 通过将速率设置为允许的值，从正常播放模式(1x)移动到特 `MediaPlayer` 技播放模式。

       请记住以下信息：
   
   * 类定 `MediaPlayerItem` 义允许的播放速率。
   * 如果不允许指定速率，TVSDK将选择最接近的允许速率。

      以下示例将播放器的内部播放速率设置为所请求的速率：

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

1. 您可以选择侦听汇率变化事件，该事件会在您请求汇率变化时以及实际发生汇率变化时通知您。

TVSDK调度与特技播放相关的以下事件：

* `MediaPlayerEvent.RATE_SELECTED`，当该值 `rate` 更改为其他值时。

* `MediaPlayerEvent.RATE_PLAYING`, when playback rescees at the selected rate.

   当播放器从特技播放模式返回到正常播放模式时，TVSDK将调度这些事件。