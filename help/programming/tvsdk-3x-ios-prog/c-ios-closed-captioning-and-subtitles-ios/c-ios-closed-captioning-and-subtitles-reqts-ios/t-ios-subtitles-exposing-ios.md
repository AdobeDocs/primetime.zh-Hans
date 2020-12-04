---
description: TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知播放器客户端内部AVAset的availableMediaCharactiesWithMediaSelectionOptions的可用性。
seo-description: TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知播放器客户端内部AVAset的availableMediaCharactiesWithMediaSelectionOptions的可用性。
seo-title: 显示字幕
title: 显示字幕
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 显示字幕{#expose-subtitles}

TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知播放器客户端内部AVAset的availableMediaCharactiesWithMediaSelectionOptions的可用性。

您可以通过`PTMediaPlayerItem`属性的`subtitlesOptions`访问可用的字幕。

显示字幕：

1. 将客户端注册为`PTMediaPlayerMediaSelectionOptionsAvailableNotification`通知的监听器。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   当您的客户端收到此通知时，`PTMediaPlayerItem`中的字幕就绪。
1. 实现与以下示例类似的`onMediaPlayerItemMediaSelectionOptionsAvailable`方法：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   有关替代音轨的信息，请参阅[替代音频](../../alternate-audio/ios-3x-alternate-audio.md)。