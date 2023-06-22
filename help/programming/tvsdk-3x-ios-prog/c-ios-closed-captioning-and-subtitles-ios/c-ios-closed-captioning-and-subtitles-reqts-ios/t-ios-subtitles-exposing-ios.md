---
description: TVSDK会使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器客户端内部AVAset的availableMediaCharacticesWithMediaSelectionOptions的可用性。
title: 公开字幕
exl-id: 42f15536-39ea-4d83-b501-b05086a0056b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 公开字幕 {#expose-subtitles}

TVSDK会使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器客户端内部AVAset的availableMediaCharacticesWithMediaSelectionOptions的可用性。

您可以通过 `PTMediaPlayerItem` 属性 `subtitlesOptions`.

要显示字幕，请执行以下操作：

1. 将客户机注册为的监听程序 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 通知。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   当您的客户收到此通知时，字幕已准备就绪， `PTMediaPlayerItem`.
1. 实施 `onMediaPlayerItemMediaSelectionOptionsAvailable` 方法类似于以下示例：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   有关备用音轨的信息，请参见  [备用音频](../../alternate-audio/ios-3x-alternate-audio.md).
