---
description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个备用音频流。
title: 访问备用音轨
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 访问备用音轨{#access-alternate-audio-tracks}

后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个备用音频流。

1. 等待MediaPlayer至少处于“已准备”状态。
1. 收听此事件：

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`：声道的初始列表可用。

1. 从获取可用的音频轨道 `MediaPlayerItem` 实例。

   `mediaPlayerItem.getAudioTracks()` 1. （可选）向用户展示可用的曲目。
1. 将选定的音轨置于 `MediaPlayerItem` 实例。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
