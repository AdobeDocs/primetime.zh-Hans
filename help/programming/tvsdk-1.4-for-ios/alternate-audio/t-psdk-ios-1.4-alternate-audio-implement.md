---
description: 后期捆绑音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个备用音频流。
title: 访问备用音轨
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 访问备用音轨{#access-alternate-audio-tracks}

后期捆绑音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个备用音频流。

1. 等待MediaPlayer至少处于 `PTMediaPlayerStatusReady` 状态。
1. 收听此事件：

   通知 `PTMediaPlayerItemMediaSelectionOptionsAvailable`：声道的初始列表可用。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 从获取可用的音频轨道 `PTMediaPlayerItem` 实例。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （可选）向用户展示可用的曲目。
1. 将选定的音轨置于 `PTMediaPlayerItem` 实例。
