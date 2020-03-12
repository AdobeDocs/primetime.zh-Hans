---
description: 您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。
seo-description: 您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。
seo-title: 保存视频位置，稍后恢复
title: 保存视频位置，稍后恢复
uuid: cff1715e-c7a9-4eda-ad71-31892c3c1e78
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 保存视频位置，稍后恢复 {#save-the-video-position-and-resume-later}

您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。

动态插入的广告在用户会话之间有所不同，因此用拼接的 **广告保存位置** ，是指将来会话中的不同位置。 TVSDK提供了在忽略拼接广告时检索播放位置的方法。

1. 当用户退出视频时，应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告持续时间。

   由于广告模式、频率限制等原因，每个会话中的广告中断可能不同。 在将来的会话中，视频在一个会话中的当前时间可能不同。 在视频中保存位置时，应用程序会检索本地时间，您可以将本地时间保存在设备上或服务器上的数据库中。

   例如，如果用户在视频的第20分钟，并且此位置包括5分钟广告，则 `getCurrentTime` 将返回1200秒，而 `getLocalTime` 此位置将返回900秒。

   >[!IMPORTANT]
   >
   >实时／线性流的本地时间和当前时间相同。 在这种情况下， `convertToLocalTime` 效果不佳。 对于VOD，播放广告时本地时间保持不变。

   ```java
   // Save the user session when player activity stops 
       @Override 
       public void onStop(){ 
           super.onStop(); 
           ... 
           prefs = PreferenceManager.getDefaultSharedPreferences( 
                                     getActivity().getApplicationContext()); 
           SharedPreferences.Editor editor = prefs.edit(); 
           // get the local time where stream stopped playing and  
           // save it in System preferences 
           editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
           editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
           editor.commit(); 
           ... 
       }
   ```

1. 恢复播放器活动时恢复用户会话。

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs =  
         PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil"). 
         equals(_contentInfo.toMediaResource().getUrl())) { 
           _lastKnownLocalTime =  
             prefs.getLong(LAST_LOCAL_TIME, 0); // get the last local time  
                                                // saved in system preferences 
           if(_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. 要在同一位置恢复视频，请执行以下操作：

   * 要从从上一会话保存的位置继续播放视频，请使用 `seekToLocalTime`。

      >[!TIP]
      >
      >仅使用本地时间值调用此方法。 如果使用当前时间结果调用该方法，则会发生错误行为。

   * 要寻找当前时间，请使用 `seek`。

1. 当应用程序收到状 `onStatusChanged` 态更改事件时，请搜索保存的本地时间。

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if(_shouldResumePlayback){ 
               if(_lastKnownLocalTime >= 0) { 
                    _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
       ... 
   }
   ```

1. 按照广告策略界面中的指定提供广告中断。
1. 通过扩展默认广告策略选择器来实施自定义广告策略选择器。
1. 提供必须通过实施向用户展示的广告中断 `selectAdBreaksToPlay`。

   该方法包括在本地时间位置之前的预卷广告中断和中卷广告中断。 您的应用程序可以决定播放前置广告中断并恢复到指定的本地时间，播放中置广告中断并恢复到指定的本地时间，或者不播放广告中断。