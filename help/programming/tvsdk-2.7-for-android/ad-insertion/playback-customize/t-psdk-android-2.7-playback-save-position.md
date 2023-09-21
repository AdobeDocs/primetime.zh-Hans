---
description: 您可以将当前播放位置保存在视频中，并在未来会话中恢复在同一位置播放。
title: 保存视频位置并在稍后恢复
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 保存视频位置并在稍后恢复 {#save-the-video-position-and-resume-later}

您可以将当前播放位置保存在视频中，并在未来会话中恢复在同一位置播放。

动态插入的广告在用户会话之间有所不同，因此保存位置 **替换为** 拼接广告是指将来会话中的不同位置。 TVSDK提供了在忽略拼接广告时检索播放位置的方法。

1. 当用户退出视频时，您的应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告持续时间。

   由于广告模式、频率上限等，每个会话中的广告时间可能会有所不同。 一个会话中视频的当前时间可能会与将来会话中的不同。 在视频中保存位置时，应用程序会检索本地时间，您可以将该时间保存在设备上或服务器上的数据库中。

   例如，如果用户位于视频的第20分钟，并且此位置包含五分钟的广告， `getCurrentTime` 将返回1200秒，而 `getLocalTime` 在此位置将返回900秒。

   >[!IMPORTANT]
   >
   >对于实时/线性流，本地时间和当前时间相同。 在本例中， `convertToLocalTime` 没有效果。 对于VOD，播放广告时本地时间保持不变。

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

1. 在播放器活动恢复时恢复用户会话。

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

1. 要在相同位置恢复视频，请执行以下操作：

   * 要从上一个会话中保存的位置恢复播放视频，请使用 `seekToLocalTime`.

     >[!TIP]
     >
     >仅使用本地时间值调用此方法。 如果使用当前时间结果调用方法，则会发生错误行为。

   * 要搜索到当前时间，请使用 `seek`.

1. 当您的应用程序收到 `onStatusChanged` 状态更改事件，搜索到保存的本地时间。

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

1. 提供在广告策略界面中指定的广告时间。
1. 通过扩展默认的广告策略选择器，实施自定义广告策略选择器。
1. 通过以下方式提供必须呈现给用户的广告时间： `selectAdBreaksToPlay`.

   此方法包括前置广告时间和中置广告时间位于本地时间位置之前。 您的应用程序可以决定播放前置广告时间并继续到指定的本地时间，播放中置广告时间并继续到指定的本地时间，或不播放广告时间。
