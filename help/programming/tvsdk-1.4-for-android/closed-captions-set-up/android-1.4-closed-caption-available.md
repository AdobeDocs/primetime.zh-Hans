---
description: 关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分作为文本显示在屏幕上。
seo-description: 关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分作为文本显示在屏幕上。
seo-title: 从可用音轨中选择当前字幕轨道
title: 从可用音轨中选择当前字幕轨道
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 53924aa8ba90555d58d15ee10fb14221c7dffaff
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---


# 从可用音轨{#select-a-current-caption-track-from-among-available-tracks}中选择当前字幕轨道

您可以从当前可用的隐藏式字幕轨道的列表中选择轨道。 这将成为当前轨道，当可见性打开时显示该轨道。 某些音轨最初可能不可用，因此请侦听表示有更多音轨可用的事件。

>[!TIP]
>
>隐藏式字幕始终处于启用状态。 所有默认的隐藏字幕轨道均被视为存在。 默认音轨（如CC1-CC4、CS1-CS6）在`ClosedCaptionsTrack.DefaultCCTypes`中枚举。 播放开始时，TVSDK会查找这些渠道中的任何一个活动。 如果找到活动，则设置该跟踪的`isActive`方法并调度`MediaPlayer.PlaybackEventListener.onUpdated`事件。

1. 等待媒体播放器处于至少PREPARED状态。
1. 聆听这些事件:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:隐藏字幕轨道的初始列表可用

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 为事件实现一个侦听器，它指示有更多可用的轨道。 当TVSDK发送事件时，请检索可用音轨的当前列表。

   每次发生列表时都检索事件，以确保您始终拥有最新的列表。
