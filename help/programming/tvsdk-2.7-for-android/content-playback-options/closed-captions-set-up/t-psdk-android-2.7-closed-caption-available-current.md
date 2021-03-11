---
description: 您可以从当前可用的隐藏字幕轨道的列表中选择轨道。 这将成为当前轨道，当可见性打开时显示。 某些轨道最初可能不可用，因此请侦听指示有更多轨道可用的事件。
title: 从可用轨道中选择当前字幕轨道
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---


# 从可用轨道{#select-a-current-caption-track-from-among-available-tracks}中选择当前字幕轨道

您可以从当前可用的隐藏字幕轨道的列表中选择轨道。 这将成为当前轨道，当可见性打开时显示。 某些轨道最初可能不可用，因此请侦听指示有更多轨道可用的事件。

1. 等待媒体播放器至少处于`PREPARED`状态。
1. 聆听以下事件:

   * `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZED`:隐藏字幕轨道的初始列表可用。

1. 获取所有当前可用的隐藏字幕轨道的列表。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 选择可用轨道作为当前轨道。

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

1. 为事件实现一个侦听器，它指示有更多的轨道可用。 当TVSDK分派事件时，检索可用轨道的当前列表。

   每次发生列表时检索事件，以确保您始终拥有最新列表。