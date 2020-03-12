---
description: 当声音听不到或观众听不到时，关闭的字幕将视频的音频部分显示为屏幕上的文本。
seo-description: 当声音听不到或观众听不到时，关闭的字幕将视频的音频部分显示为屏幕上的文本。
seo-title: 从可用音轨中选择当前字幕轨道
title: 从可用音轨中选择当前字幕轨道
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 从可用音轨中选择当前字幕轨道{#select-a-current-caption-track-from-among-available-tracks}

您可以从当前可用的隐藏式字幕轨道列表中选择轨道。 这将成为当前轨道，当可见性打开时显示。 某些音轨最初可能不可用，因此请侦听指示有更多音轨可用的事件。

>[!TIP]
>
>隐藏式字幕始终处于启用状态。 所有默认的隐藏式字幕轨道均被视为存在。 默认音轨（如CC1-CC4、CS1-CS6）在中进行枚举 `ClosedCaptionsTrack.DefaultCCTypes`。 当播放开始时，TVSDK会查找这些频道中的任何一个频道的活动。 如果发现活动，则设置该 `isActive` 跟踪的方法并调度该事 `MediaPlayer.PlaybackEventListener.onUpdated` 件。

1. 等待媒体播放器处于至少PREPARED状态。
1. 聆听以下活动：

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:隐藏式字幕轨道的初始列表可用

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
   
<b>mediaPlayer.getCurrentItem()。selectClosedCaptionsTrack(track);</b>selectedClosedCaptionsIndex = i;}}

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

