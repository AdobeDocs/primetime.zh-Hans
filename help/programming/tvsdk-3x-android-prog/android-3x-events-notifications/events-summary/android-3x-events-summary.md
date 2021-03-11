---
description: 您的应用程序可以监听TVSDK调度的活动，以监视播放器中的事件和播放器不断变化的状态。
title: Primetime播放器事件摘要
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Primetime播放器事件摘要{#primetime-player-events-summary}

您的应用程序可以监听TVSDK调度的活动，以监视播放器中的事件和播放器不断变化的状态。

## 事件{#events}

TVSDK会在事件发生时通知您，您的应用程序必须对其做出响应。 每个事件都对应一个侦听器类，它有一个必须实现的回调方法。

>[!TIP]
>
>事件代码是`MediaPlayerEvent`枚举的常量。

`AdBreakCompletedEventListener`

* **意** 义广告分段的播放完成。

* **要实现的回调** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **意** 义在播放过程中跳过了广告中断。

* **要实现的回调** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **意** 义广告中断的播放已开始。

* **要实现的回调** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_START`

`AdClickedEventListener`

* **意** 义在播放过程中单击了广告。

* **要实现的回调** `onAdClicked(AdClickEvent event)`
* **事件代码** `AD_CLICK`

`AdCompletedEventListener`

* **意** 义广告播放完成。

* **要实现的回调** `onAdCompleted(AdPlaybackEvent event)`

* **事件代码** `AD_COMPLETE`

`AdProgressEventListener`

* **MeaningReporting** 播放过程。

* **要实现的回调** `onAdProgress(AdPlaybackEvent event)`

* **事件代码** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **意** 义Primetime广告决策广告解决已完成。此事件仅适用于VOD内容。

* **要实现的回调** `onAdResolutionComplete()`

* **事件代码** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意** 义广告的播放已开始。

* **要实现的回调** `onAdStarted(AdPlaybackEvent event)`

* **事件代码** `AD_START`

`AudioUpdatedEventListener`

* **意** 义检测到新音轨。

* **要实现的回调** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代码** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **意** 义播放器已开始缓冲。

* **要实现的回调** `onBufferingBegin(BufferEvent event)`

* **事件代码** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **意** 义播放器已停止缓冲。

* **要实现的回调** `onBufferingEnd(BufferEvent event)`

* **事件代码** `BUFFERING_END`

&#39;BufferPreparedEventListener&quot;

* **意** 义缓冲区已准备。

* **要实现的回调** `onBufferPrepared()`

* **事件代码** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **意** 义已检测到新的题注轨道。

* **要实现的回调** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代码** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **意** 义在媒体流中检测到新的DRM元数据。

* **要实现的回调** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代码** `DRM_METADATA`

`ItemCreatedEventListener`

* **意** 义已创建新的媒体播放器项。

* **要实现的回调** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **已** 为当前项目创建新加载信息。

* **要实现的回调** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_UPDATED`

`LoadInformationEventListener`

* **意** 义已加载新区段。

* **要实现的回调** `onLoadInformation(LoadInformationEvent event)`

* **事件代码** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Meaning** 主清单或播放列表已更新。

* **要实现的回调** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代码** `MANIFEST_UPDATED`

`NotificationEventListener`

* **意** 义操作失败。

* **要实现的回调** `onNotification(NotificationEvent event)`

* **事件代码** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **意** 义播放范围已更新。

* **要实现的回调** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代码** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **意** 味在屏幕上显示新的播放速率。

* **要实现的回调** `onRatePlaying(PlaybackRateEvent event)`

* **事件代码** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **意** 义已设置MediaPlayer的rate属性。

* **要实现的回调** `onRateSelected(PlaybackRateEvent event)`

* **事件代码** `RATE_SELECTED`

`PlayStartEventListener`

* **意** 义播放已开始。

* **要实现的回调** `onPlayStart()`

* **事件代码** `PLAY_START`

`ProfileChangeEventListener`

* **意** 义MediaPlayer的当前用户档案已更改。

* **要实现的回调** `onProfileChanged(ProfileEvent event)`

* **事件代码** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **MeaningPlayback** 达到时间轴保留。

* **要实现的回调** `onReservationReached(ReservationEvent event)`

* **事件代码** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **MeaningSeek** 操作已启动。

* **要实现的回调** `onSeekBegin(SeekEvent event)`

* **事件代码** `SEEK_BEGIN`

`SeekEndEventListener`

* **意** 义搜索操作已完成。

* **要实现的回调** `onSeekEnd(SeekEvent event)`

* **事件代码** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **意** 义由于内部播放规则或外部业务规则，搜索位置已调整。

* **要实现的回调** `onPositionAdjusted(SeekEvent event)`

* **事件代码** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **意** 义可用媒体的大小。

* **要实现的回调** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代码** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **意** 义MediaPlayer状态已更改。

* **要实现的回调** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代码** `STATUS_CHANGED`

`TimeChangeEventListener`

* **意** 义播放指示器已更改。

* **要实现的回调** `onTimeChanged(TimeChangeEvent event)`

* **事件代码** `TIME_CHANGED`

`TimedEventEventListener`

* **意** 义操作已完成，且操作所花费的时间。

* **要实现的回调** `onTimedEvent(TimedEventEvent event)`

* **事件代码** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **意** 义已将新的定时元数据添加到后台项目。

* **要实现的回调** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **意** 义在媒体流中检测到新的定时元数据。

* **要实现的回调** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **意** 义时间轴已修改。可能已在时间轴中添加或删除广告。

* **要实现的回调** `onTimelineUpdated(TimelineEvent event)`

* **事件代码** `TIMELINE_UPDATED`