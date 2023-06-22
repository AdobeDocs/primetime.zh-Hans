---
description: 备用音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个备用音频流。
title: 访问备用音轨
exl-id: e5f5b943-4886-4884-80d2-225b5c7e3aed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 访问备用音轨 {#access-alternate-audio-tracks}

备用音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个备用音频流。

1. 等待 `MediaPlayer` 至少在 `MediaPlayerStatus.PREPARED` 状态。
1. 聆听 `MediaPlayerEvent.STATUS_CHANGED` 具有状态的事件 `MediaPlayerStatus.PREPARED`.

   此步骤表示声道的初始列表可用。

1. 从获取可用的音频曲目 `MediaPlayerItem` 实例。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （可选）向用户显示可用曲目。
1. 将选定的音轨设置为 `MediaPlayerItem` 实例。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
