---
description: 替代音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 替代音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问替代音轨
title: 访问替代音轨
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 访问替代音轨 {#access-alternate-audio-tracks}

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

