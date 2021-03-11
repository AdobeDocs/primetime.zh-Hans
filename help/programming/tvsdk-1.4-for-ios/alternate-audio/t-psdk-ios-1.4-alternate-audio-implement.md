---
description: 延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定的、可包含多个替代音频流的视频。
title: 访问备用音轨
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 访问备用音轨{#access-alternate-audio-tracks}

延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定的、可包含多个替代音频流的视频。

1. 等待MediaPlayer至少处于`PTMediaPlayerStatusReady`状态。
1. 听听此事件:

   通知`PTMediaPlayerItemMediaSelectionOptionsAvailable`:音轨的初始列表可用。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 从`PTMediaPlayerItem`实例获取可用的音轨。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （可选）向用户显示可用音轨。
1. 在`PTMediaPlayerItem`实例上设置所选音轨。
