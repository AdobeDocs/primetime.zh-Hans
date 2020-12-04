---
description: 备用音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个备用音频流的视频。
seo-description: 备用音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个备用音频流的视频。
seo-title: 访问备用音轨
title: 访问备用音轨
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# 访问备用音轨{#access-alternate-audio-tracks}

备用音频使用MediaPlayer播放在M3U8 HLS播放列表中指定并可包含多个备用音频流的视频。

1. 等待`MediaPlayer`至少处于`MediaPlayerStatus.PREPARED`状态。
1. 侦听状态为`MediaPlayerStatus.PREPARED`的`MediaPlayerEvent.STATUS_CHANGED`事件。

   此步骤意味着音轨的初始列表可用。

1. 从`MediaPlayerItem`实例获取可用的音轨。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （可选）向用户显示可用的音轨。
1. 在`MediaPlayerItem`实例上设置所选音轨。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
