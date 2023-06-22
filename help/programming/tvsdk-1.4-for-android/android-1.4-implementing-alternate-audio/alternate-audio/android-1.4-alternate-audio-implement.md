---
description: 后期捆绑音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个替代音频流。
title: 访问备用音轨
exl-id: d357bcc9-2996-42f0-a733-482f59e938ac
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 访问备用音轨{#access-alternate-audio-tracks}

后期捆绑音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个替代音频流。

1. 等待MediaPlayer至少处于PREPARED状态。
1. 收听此事件：

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`：可用初始音频曲目列表。

1. 从获取可用的音频曲目 `MediaPlayerItem` 实例。

   `mediaPlayerItem.getAudioTracks()` 1. （可选）向用户显示可用曲目。
1. 将选定的音轨设置为 `MediaPlayerItem` 实例。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
