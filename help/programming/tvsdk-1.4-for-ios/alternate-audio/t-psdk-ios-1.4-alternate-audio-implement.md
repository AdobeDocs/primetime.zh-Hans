---
description: 延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 延迟绑定音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问备用音轨
title: 访问备用音轨
uuid: 77e39633-bf17-4a06-a2a1-93fdaadedd17
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
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
