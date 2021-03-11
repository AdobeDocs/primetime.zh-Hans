---
description: 您可以在视频中保存当前播放位置，并在将来的会话中在相同位置继续播放。
title: 保存视频位置并稍后恢复
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# 保存视频位置并稍后恢复{#save-the-video-position-and-resume-later}

您可以在视频中保存当前播放位置，并在将来的会话中在相同位置继续播放。

动态插入的广告在用户会话之间有所不同，因此将位置&#x200B;**与**&#x200B;拼接的广告保存后，将在将来会话中的位置不同。 TVSDK提供方法来检索播放位置，同时忽略拼接的广告。

1. 当用户退出视频时，您的应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告期。

   由于广告模式、频率限制等原因，每个会话中的广告中断可能会有所不同。 在将来的会话中，视频在一个会话中的当前时间可能有所不同。 在视频中保存位置时，应用程序会检索本地时间，您可以将本地时间保存到设备上或服务器上的数据库中。

   例如，如果用户在视频的第20分钟，且此位置包含5分钟广告，则`getCurrentTime`将返回1200秒，而此位置的`getLocalTime`将返回900秒。

   >[!IMPORTANT]
   >
   >实时/线性流的本地时间和当前时间相同。 在这种情况下，`convertToLocalTime`不起作用。 对于VOD，播放广告时本地时间保持不变。

   ```java
   // Save the user session when player activity stops 
   @Override 
   public void onStop() { 
       super.onStop(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences( 
                 getActivity().getApplicationContext() 
               ); 
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
       prefs = PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil").equals(_contentInfo.toMediaResource().getUrl())) { 
   
           _lastKnownLocalTime = prefs.getLong(LAST_LOCAL_TIME, 0);    // get the last local time saved  
                                                                       // in system preferences 
           if (_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. 要在同一位置恢复视频，请执行以下操作：

   * 要从从上一会话中保存的位置继续播放视频，请使用`seekToLocalTime`。

      >[!TIP]
      >
      >只使用本地时间值调用此方法。 如果使用当前时间结果调用该方法，则会发生错误行为。

   * 要查找当前时间，请使用`seek`。

1. 当应用程序收到`onStatusChanged`状态更改事件时，请查找保存的本地时间。

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if (_shouldResumePlayback) { 
               if(_lastKnownLocalTime >= 0) { 
                   _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
        ... 
   } 
   ```

1. 按照广告策略接口中的指定提供广告中断。
1. 通过扩展默认广告策略选择器来实施自定义广告策略选择器。
1. 通过实施`selectAdBreaksToPlay`提供必须向用户显示的广告分段。

   该方法包括在本地时间位置之前的前卷广告中断和中间广告中断。 您的应用程序可以决定播放前置广告中断，并恢复到指定的本地时间，播放中间广告中断，恢复到指定的本地时间，或者不播放广告中断。
