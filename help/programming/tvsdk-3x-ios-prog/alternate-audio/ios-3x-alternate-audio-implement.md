---
description: 后期捆绑音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个替代音频流。
title: 访问备用音轨
exl-id: c95e2bae-fcf3-4ae2-be11-fb3191b380f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 访问备用音轨 {#access-alternate-audio-tracks}

后期捆绑音频使用PTMediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个替代音频流。

1. 等待MediaPlayer至少处于 `PTMediaPlayerStatusReady` 状态。
1. 收听此事件：

   通知 `PTMediaPlayerItemMediaSelectionOptionsAvailable`：可用初始音频曲目列表。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 从获取可用的音频曲目 `PTMediaPlayerItem` 实例。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （可选）向用户显示可用曲目。
1. 将选定的音轨设置为 `PTMediaPlayerItem` 实例。
