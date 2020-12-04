---
description: 延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问备用音轨
title: 访问备用音轨
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 访问备用音轨{#access-alternate-audio-tracks}

延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。

1. 请等待MediaPlayer至少处于`PTMediaPlayerStatusReady`状态。
1. 聆听此事件:

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

1. （可选）向用户显示可用的音轨。
1. 在`PTMediaPlayerItem`实例上设置所选音轨。
