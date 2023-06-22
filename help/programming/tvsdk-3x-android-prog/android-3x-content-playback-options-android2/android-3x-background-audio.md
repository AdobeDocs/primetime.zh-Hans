---
title: 启用背景音频
description: 启用背景音频
copied-description: true
exl-id: 5bb72233-27d0-4968-b32c-c8d5ac5ac8c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 启用背景音频 {#enable-background-audio}

要在应用程序处于后台时启用音频播放，应用程序应调用 `enableAudioPlaybackInBackground` 当播放器处于“已准备”状态时，将true作为参数的MediaPlayer API。

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

当应用程序在响应电话等事件期间失去对音频焦点的保持时，应暂停播放。 以下代码段演示了如何实施 `OnAudioFocusChangeListener`：

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
