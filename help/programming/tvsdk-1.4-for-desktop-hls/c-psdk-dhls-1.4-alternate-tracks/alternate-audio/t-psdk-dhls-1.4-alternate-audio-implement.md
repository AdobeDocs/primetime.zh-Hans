---
description: 延迟绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的、可包含多个替代音频流的视频。
title: 访问备用音轨
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 访问备用音轨{#access-alternate-audio-tracks}

延迟绑定音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的、可包含多个替代音频流的视频。

1. 等待`MediaPlayer`至少处于PREPARED状态。
1. 聆听以下事件:

   * `MediaPlayerItemEvent.ITEM_CREATED`:音轨的初始列表可用。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:在播放期间音轨发生更改

1. 从`MediaPlayerItem`实例获取可用的音轨。
1. （可选）向用户显示可用音轨。
1. 在`MediaPlayerItem`实例上设置所选音轨。
