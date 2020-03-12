---
description: 后期绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 后期绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问替代音轨
title: 访问替代音轨
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 访问替代音轨 {#access-alternate-audio-tracks}

后期绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。

1. 等待MediaPlayer至少处于状 `PTMediaPlayerStatusReady` 态。
1. 侦听此事件：

   通知 `PTMediaPlayerItemMediaSelectionOptionsAvailable`:音轨的初始列表可用。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 从实例中获取可用的音 `PTMediaPlayerItem` 轨。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （可选）向用户显示可用的音轨。
1. 在实例上设置选定的音 `PTMediaPlayerItem` 轨。
