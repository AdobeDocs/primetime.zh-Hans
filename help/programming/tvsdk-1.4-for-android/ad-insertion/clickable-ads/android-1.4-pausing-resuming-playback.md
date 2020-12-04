---
description: 当用户单击广告时，您的应用程序应暂停主视频内容的播放。
seo-description: 当用户单击广告时，您的应用程序应暂停主视频内容的播放。
seo-title: 暂停和恢复播放
title: 暂停和恢复播放
uuid: a8fec392-3a71-4086-abf1-23522d023680
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# 暂停并恢复播放{#pause-and-resume-playback}

当用户单击广告时，您的应用程序应暂停主视频内容的播放。

从Android活动覆盖`onPause`和`onResume`。

```java
@Override 
public void onResume() { 
    super.onResume(); 
    requestAudioFocus(); 
    if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
        _mediaPlayer.play(); 
    } 
} 
... 
 
@Override 
public void onPause() { 
    super.onPause(); 
    if (_mediaPlayer != null) { 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
          _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
            _savedPlayerState = _mediaPlayer.getStatus(); 
            _lastKnownTime = _mediaPlayer.getCurrentTime(); 
        } 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
            _mediaPlayer.pause(); 
            _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
        } 
    } 
} 
 
abandonAudioFocus(); 
```

