---
description: 隐藏式字幕在声音无法听见或观看者听力缺佳时将视频的音频部分显示为文本。
title: 从可用字幕轨道中选择当前字幕轨道
exl-id: 75970604-c318-4621-bad3-caab292c8a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 从可用字幕轨道中选择当前字幕轨道{#select-a-current-caption-track-from-among-available-tracks}

您可以从当前可用的隐藏式字幕字幕字幕的列表中选择一个字幕。 这将成为当前轨道，当可见性打开时将显示该轨道。 某些跟踪最初可能不可用，因此请监听指示有更多跟踪可用的事件。

>[!TIP]
>
>隐藏式字幕始终处于启用状态。 所有默认的隐藏式字幕字幕都被视为存在。 默认磁道（如CC1-CC4、CS1-CS6）枚举于 `ClosedCaptionsTrack.DefaultCCTypes`. 当播放开始时，TVSDK会在任何这些渠道上查找活动。 如果找到活动，则会设置 `isActive` 方法以跟踪和分发 `MediaPlayer.PlaybackEventListener.onUpdated` 事件。

1. 等待媒体播放器至少处于PREPARED状态。
1. 收听以下事件：

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`：提供了隐藏式字幕跟踪的初始列表

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 为事件实施侦听器，以指示有更多的可用跟踪。 当TVSDK调度事件时，检索可用磁道的当前列表。

   每次发生事件时都检索该列表，以确保您始终拥有最新的列表。
