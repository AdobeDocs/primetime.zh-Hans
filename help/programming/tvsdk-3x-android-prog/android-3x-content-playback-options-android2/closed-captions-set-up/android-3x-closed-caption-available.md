---
description: 您可以从当前可用的隐藏式字幕轨道的列表中选择轨道。 这将成为当前轨道，当可见性打开时显示该轨道。 某些音轨最初可能不可用，因此请侦听表示有更多音轨可用的事件。
seo-description: 您可以从当前可用的隐藏式字幕轨道的列表中选择轨道。 这将成为当前轨道，当可见性打开时显示该轨道。 某些音轨最初可能不可用，因此请侦听表示有更多音轨可用的事件。
seo-title: 从可用音轨中选择当前字幕轨道
title: 从可用音轨中选择当前字幕轨道
uuid: ee2bda5e-e398-4d09-bc5c-5a6adbf5f603
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# 从可用音轨{#select-a-current-caption-track-from-among-available-tracks}中选择当前字幕轨道

您可以从当前可用的隐藏式字幕轨道的列表中选择轨道。 这将成为当前轨道，当可见性打开时显示该轨道。 某些音轨最初可能不可用，因此请侦听表示有更多音轨可用的事件。

1. 等待媒体播放器至少处于`PREPARED`状态。
1. 聆听这些事件:

   * `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZED`:隐藏字幕轨道的初始列表可用。

1. 获取所有当前可用的隐藏字幕轨道的列表。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 选择可用的轨道作为当前轨道。

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

1. 为事件实现一个侦听器，它指示有更多可用的轨道。 当TVSDK发送事件时，请检索可用音轨的当前列表。

   每次发生列表时都检索事件，以确保您始终拥有最新的列表。