---
description: TVSDK会使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器客户端内部AVAset的availableMediaCharactifilesWithMediaSelectionOptions的可用性。
title: 公开字幕
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 公开字幕 {#expose-subtitles}

TVSDK会使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器客户端内部AVAset的availableMediaCharactifilesWithMediaSelectionOptions的可用性。

您可以通过 `PTMediaPlayerItem` 属性的 `subtitlesOptions`.

要显示字幕，请执行以下操作：

1. 将客户机注册为监听程序 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 通知。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   当您的客户收到此通知时，字幕已准备就绪，位于 `PTMediaPlayerItem`.
1. 实施 `onMediaPlayerItemMediaSelectionOptionsAvailable` 方法类似于以下示例：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   有关备用声道的信息，请参阅  [备用音频](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
