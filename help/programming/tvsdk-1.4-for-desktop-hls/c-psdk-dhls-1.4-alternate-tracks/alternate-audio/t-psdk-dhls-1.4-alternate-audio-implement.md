---
description: 后期捆绑音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个替代音频流。
title: 访问备用音轨
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 访问备用音轨{#access-alternate-audio-tracks}

后期捆绑音频使用MediaPlayer播放在M3U8 HLS播放列表中指定的视频，该视频可以包含多个替代音频流。

1. 等待 `MediaPlayer` 至少处于“已准备”状态。
1. 收听以下事件：

   * `MediaPlayerItemEvent.ITEM_CREATED`：可用初始音频曲目列表。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`：播放期间更改了音频轨道

1. 从获取可用的音频曲目 `MediaPlayerItem` 实例。
1. （可选）向用户显示可用曲目。
1. 将选定的音轨设置为 `MediaPlayerItem` 实例。
