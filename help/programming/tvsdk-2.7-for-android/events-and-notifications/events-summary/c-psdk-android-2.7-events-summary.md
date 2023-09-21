---
description: 您的应用程序可以通过侦听由TVSDK调度的事件，监控播放器中的活动和播放器状态的变化。
title: Primetime播放器事件摘要
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Primetime播放器事件摘要 {#primetime-player-events-summary-overview}

您的应用程序可以通过侦听由TVSDK调度的事件，监控播放器中的活动和播放器状态的变化。

## 活动 {#events}

TVSDK会在发生应用程序必须响应的事件时通知您。 每个事件都对应一个监听程序类，其中包含必须实现的回调方法。

>[!TIP]
>
>事件代码是 `MediaPlayerEvent` 枚举。

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* **含义**广告时间的播放结束。

* **回调以实施** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* **表示**播放期间跳过了一个广告时间。

* **回调以实施** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* **含义**广告时间的播放已开始。

* **回调以实施** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* **含义**广告在播放过程中被点击。

* **回调以实施** `onAdClicked(AdClickEvent event)`

* **事件代码** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* **含义**广告播放结束。

* **回调以实施** `onAdCompleted(AdPlaybackEvent event)`

* **事件代码** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* **表示**播放期间报告进度。

* **回调以实施** `onAdProgress(AdPlaybackEvent event)`

* **事件代码** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ****示Primetime ad decisioningad解析已完成。 此事件仅适用于VOD内容。

* **回调以实施** `onAdResolutionComplete()`

* **事件代码** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* **含义**广告播放已开始。

* **回调以实施** `onAdStarted(AdPlaybackEvent event)`

* **事件代码** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* **含义**检测到新的音频轨道。

* **回调以实施** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代码** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* **含义**播放器已开始缓冲。

* **回调以实施** `onBufferingBegin(BufferEvent event)`

* **事件代码** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* **表示**播放器已停止缓冲。

* **回调以实施** `onBufferingEnd(BufferEvent event)`

* **事件代码** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* **含义**缓冲已准备就绪。

* **回调以实施** `onBufferPrepared()`

* **事件代码** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* **含义**检测到新的字幕跟踪。

* **回调以实施** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代码** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* **含义**已在媒体流中检测到新的DRM元数据。

* **回调以实施** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代码** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* **含义**已创建新的媒体播放器项目。

* **回调以实施** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* **含义**已为当前项目创建新的负荷信息。

* **回调以实施** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* **表示**加载了新区段。

* **回调以实施** `onLoadInformation(LoadInformationEvent event)`

* **事件代码** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* **含义**主清单或播放列表已更新。

* **回调以实施** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代码** `MANIFEST_UPDATED`

## NotificationeventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* **含义**操作失败。

* **回调以实施** `onNotification(NotificationEvent event)`

* **事件代码** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* **含义**播放范围已更新。

* **回调以实施** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代码** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* **含义**新的播放速率在屏幕上可见。

* **回调以实施** `onRatePlaying(PlaybackRateEvent event)`

* **事件代码** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ****示MediaPlayer的速率属性已设置。

* **回调以实施** `onRateSelected(PlaybackRateEvent event)`

* **事件代码** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* **含义**播放已开始。

* **回调以实施** `onPlayStart()`

* **事件代码** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* **表示**MediaPlayer的当前配置文件已更改。

* **回调以实施** `onProfileChanged(ProfileEvent event)`

* **事件代码** `PROFILE_CHANGED`

## ReservationReactedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* **表示播放**达到时间线预留。

* **回调以实施** `onReservationReached(ReservationEvent event)`

* **事件代码** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* **表示搜**操作已开始。

* **回调以实施** `onSeekBegin(SeekEvent event)`

* **事件代码** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* **含义**搜寻操作已完成。

* **回调以实施** `onSeekEnd(SeekEvent event)`

* **事件代码** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* **含义**由于内部播放规则或外部业务规则，搜寻位置已调整。

* **回调以实施** `onPositionAdjusted(SeekEvent event)`

* **事件代码** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* **含义**介质的大小可用。

* **回调以实施** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代码** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* **表**MediaPlayer状态已更改。

* **回调以实施** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代码** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* **含义**播放头已更改。

* **回调以实施** `onTimeChanged(TimeChangeEvent event)`

* **事件代码** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* **含义**操作已完成，且所用时间也各不相同。

* **回调以实施** `onTimedEvent(TimedEventEvent event)`

* **事件代码** `TIMED_EVENT`

## TimelineMetadataAddInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* **含义**新的定时元数据已添加到后台项目。

* **回调以实施** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* **含义**在媒体流中检测到新的定时元数据。

* **回调以实施** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatesEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* **表示**时间线已被修改。 广告可能已添加到时间轴或从时间轴中删除。

* **回调以实施** `onTimelineUpdated(TimelineEvent event)`

* **事件代码** `TIMELINE_UPDATED`
