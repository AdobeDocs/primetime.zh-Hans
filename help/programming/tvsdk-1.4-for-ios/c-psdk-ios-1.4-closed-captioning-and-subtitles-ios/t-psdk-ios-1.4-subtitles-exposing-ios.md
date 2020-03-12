---
description: TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知您的播放器客户端内部AVAset的availableMediaCharatiersWithMediaSelectionOptions的可用性。
seo-description: TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知您的播放器客户端内部AVAset的availableMediaCharatiersWithMediaSelectionOptions的可用性。
seo-title: 显示字幕
title: 显示字幕
uuid: 657ab9c7-b205-4d13-81a7-51bc8e7d5ee2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 显示字幕 {#expose-subtitles}

TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知您的播放器客户端内部AVAset的availableMediaCharatiersWithMediaSelectionOptions的可用性。

您可以通过属性访问可用 `PTMediaPlayerItem` 的字幕 `subtitlesOptions`。

显示字幕：

1. 将客户端注册为通知的监听 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 器。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   当您的客户收到此通知时，将在中显示字幕 `PTMediaPlayerItem`。
1. 实现与 `onMediaPlayerItemMediaSelectionOptionsAvailable` 以下示例类似的方法：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   有关替代音轨的信息，请参阅 [替代音频](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md)。