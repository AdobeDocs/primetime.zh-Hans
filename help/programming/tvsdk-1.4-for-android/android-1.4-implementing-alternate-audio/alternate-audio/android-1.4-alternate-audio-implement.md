---
description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问替代音轨
title: 访问替代音轨
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 访问替代音轨{#access-alternate-audio-tracks}

后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。

1. 等待MediaPlayer至少处于PREPARED状态。
1. 侦听此事件：

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:音轨的初始列表可用。

1. 从实例中获取可用的音 `MediaPlayerItem` 轨。

   `mediaPlayerItem.getAudioTracks()` 1. （可选）向用户显示可用的音轨。
1. 在实例上设置选定的音 `MediaPlayerItem` 轨。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`