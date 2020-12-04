---
description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问备用音轨
title: 访问备用音轨
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# 访问备用音轨{#access-alternate-audio-tracks}

后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。

1. 等待MediaPlayer至少处于PREPARED状态。
1. 聆听此事件:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:音轨的初始列表可用。

1. 从`MediaPlayerItem`实例获取可用的音轨。

   `mediaPlayerItem.getAudioTracks()` 1. （可选）向用户显示可用的音轨。
1. 在`MediaPlayerItem`实例上设置所选音轨。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`