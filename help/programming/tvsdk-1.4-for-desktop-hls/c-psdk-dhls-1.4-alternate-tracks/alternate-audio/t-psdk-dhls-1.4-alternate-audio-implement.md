---
description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-description: 后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。
seo-title: 访问替代音轨
title: 访问替代音轨
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 访问替代音轨{#access-alternate-audio-tracks}

后期绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个替代音频流的视频。

1. 请等待 `MediaPlayer` 至少处于“PREPARED”状态。
1. 聆听以下活动：

   * `MediaPlayerItemEvent.ITEM_CREATED`:音轨的初始列表可用。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:回放期间音轨发生更改

1. 从实例中获取可用的音 `MediaPlayerItem` 轨。
1. （可选）向用户显示可用的音轨。
1. 在实例上设置选定的音 `MediaPlayerItem` 轨。
