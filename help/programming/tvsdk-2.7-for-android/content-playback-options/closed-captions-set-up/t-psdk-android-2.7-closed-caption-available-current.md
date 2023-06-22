---
description: 您可以从当前可用的隐藏式字幕字幕字幕的列表中选择一个字幕。 这将成为当前轨道，当可见性打开时将显示该轨道。 某些跟踪最初可能不可用，因此请监听指示有更多跟踪可用的事件。
title: 从可用字幕轨道中选择当前字幕轨道
exl-id: d604dedc-f3c3-4c97-9b0f-84da326c0678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 从可用字幕轨道中选择当前字幕轨道 {#select-a-current-caption-track-from-among-available-tracks}

您可以从当前可用的隐藏式字幕字幕字幕的列表中选择一个字幕。 这将成为当前轨道，当可见性打开时将显示该轨道。 某些跟踪最初可能不可用，因此请监听指示有更多跟踪可用的事件。

1. 等待媒体播放器至少处于 `PREPARED` 状态。
1. 收听以下事件：

   * `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZED`：提供了隐藏式字幕字幕跟踪的初始列表。

1. 获取所有当前可用的隐藏式字幕字幕的列表。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 选择一个可用的曲目作为当前曲目。

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

1. 为事件实施侦听器，以指示有更多的可用跟踪。 当TVSDK调度事件时，检索可用磁道的当前列表。

   每次发生事件时都检索该列表，以确保您始终拥有最新的列表。
