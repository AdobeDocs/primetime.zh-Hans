---
description: 当用户单击广告时，您的应用程序应暂停主视频内容的播放。
seo-description: 当用户单击广告时，您的应用程序应暂停主视频内容的播放。
seo-title: 暂停和恢复播放
title: 暂停和恢复播放
uuid: 87ba9f05-912d-4b85-8add-feb26a796a3a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# 暂停并恢复播放{#pause-and-resume-playback}

当用户单击广告时，您的应用程序应暂停主视频内容的播放。

1. 从Android活动覆盖`onPause`和`onResume`。

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```

