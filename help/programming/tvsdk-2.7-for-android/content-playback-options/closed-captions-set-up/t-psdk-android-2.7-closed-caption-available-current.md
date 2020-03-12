---
description: 您可以从当前可用的隐藏式字幕轨道列表中选择轨道。 这将成为当前轨道，当可见性打开时显示。 某些音轨最初可能不可用，因此请侦听指示有更多音轨可用的事件。
seo-description: 您可以从当前可用的隐藏式字幕轨道列表中选择轨道。 这将成为当前轨道，当可见性打开时显示。 某些音轨最初可能不可用，因此请侦听指示有更多音轨可用的事件。
seo-title: 从可用音轨中选择当前字幕轨道
title: 从可用音轨中选择当前字幕轨道
uuid: d582779a-2789-4e2a-85f6-1a0b9b847382
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 从可用音轨中选择当前字幕轨道 {#select-a-current-caption-track-from-among-available-tracks}

您可以从当前可用的隐藏式字幕轨道列表中选择轨道。 这将成为当前轨道，当可见性打开时显示。 某些音轨最初可能不可用，因此请侦听指示有更多音轨可用的事件。

1. 等待媒体播放器至少处于状态 `PREPARED` 。
1. 聆听以下活动：

   * `MediaPlayerEvent.STATUS_CHANGED` 状态为 `MediaPlayerStatus.INITIALIZED`:隐藏式字幕轨道的初始列表可用。

1. 获取当前所有可用隐藏式字幕轨道的列表。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 选择一个可用的轨道作为当前轨道。

   例如：

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 为指示有更多磁道可用的事件实现监听器。 当TVSDK分派该事件时，请检索可用轨道的当前列表。

   每次发生事件时检索列表，以确保您始终拥有最新列表。