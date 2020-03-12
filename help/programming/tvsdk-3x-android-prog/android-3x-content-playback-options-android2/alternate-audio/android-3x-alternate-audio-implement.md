---
description: 替代音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 替代音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问替代音轨
title: 访问替代音轨
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 访问替代音轨{#access-alternate-audio-tracks}

替代音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。

1. 等待 `MediaPlayer` 至少处于状 `MediaPlayerStatus.PREPARED` 态。
1. 以状态 `MediaPlayerEvent.STATUS_CHANGED` 侦听活动 `MediaPlayerStatus.PREPARED`。

   此步骤表示音轨的初始列表可用。

1. 从实例中获取可用的音 `MediaPlayerItem` 轨。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （可选）向用户显示可用的音轨。
1. 在实例上设置选定的音 `MediaPlayerItem` 轨。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
