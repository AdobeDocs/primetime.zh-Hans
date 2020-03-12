---
description: 您的应用程序可以监视播放器中的活动，以及播放器状态的变化，方法是侦听TVSDK调度的事件。
seo-description: 您的应用程序可以监视播放器中的活动，以及播放器状态的变化，方法是侦听TVSDK调度的事件。
seo-title: Primetime播放器活动摘要
title: Primetime播放器活动摘要
uuid: ed3be4c2-8df3-4d96-a30b-74c196262798
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# Primetime播放器活动摘要 {#primetime-player-events-summary-overview}

您的应用程序可以监视播放器中的活动，以及播放器状态的变化，方法是侦听TVSDK调度的事件。

## 活动 {#events}

TVSDK会在应用程序必须响应的事件发生时通知您。 每个事件都对应一个监听器类，并且有一个必须实现的回调方法。

>[!TIP]
>
>事件代码是枚举的常 `MediaPlayerEvent` 数。

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* **意思**广告中断的播放完成。

* **实施回调** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **活动代码** `AD_BREAK_COMPLETE`

## AdBreakBrippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* **意味着**在播放过程中跳过广告中断。

* **实施回调** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **活动代码** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* **含义**广告中断播放已开始。

* **实施回调** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **活动代码** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* **意味着**在播放过程中单击了广告。

* **实施回调** `onAdClicked(AdClickEvent event)`

* **活动代码** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* **含义**广告播放完成。

* **实施回调** `onAdCompleted(AdPlaybackEvent event)`

* **活动代码** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* **含义**在播放期间报告进度。

* **实施回调** `onAdProgress(AdPlaybackEvent event)`

* **活动代码** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* **含义** Primetime广告决策广告解决方案已完成。 此活动仅适用于VOD内容。

* **实施回调** `onAdResolutionComplete()`

* **活动代码** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* **含义**广告播放已开始。

* **实施回调** `onAdStarted(AdPlaybackEvent event)`

* **活动代码** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* **含义**已检测到新的音轨。

* **实施回调** `onAudioUpdated(MediaPlayerItemEvent event)`

* **活动代码** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* **含义**播放器已开始缓冲。

* **实施回调** `onBufferingBegin(BufferEvent event)`

* **活动代码** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* **含义**播放器已停止缓冲。

* **实施回调** `onBufferingEnd(BufferEvent event)`

* **活动代码** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* **含义**准备缓冲区。

* **实施回调** `onBufferPrepared()`

* **活动代码** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* **含义**检测到新的字幕轨道。

* **实施回调** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **活动代码** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* **含义**在媒体流中检测到新的DRM元数据。

* **实施回调** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **活动代码** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* **含义**已创建新的媒体播放器项目。

* **实施回调** `onItemCreated(MediaPlayerItemEvent event)`

* **活动代码** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* **含义**已为当前项目创建新的加载信息。

* **实施回调** `onLoadComplete(MediaPlayerItemEvent event)`

* **活动代码** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* **含义**已加载新区段。

* **实施回调** `onLoadInformation(LoadInformationEvent event)`

* **活动代码** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* **含义**主清单或播放列表已更新。

* **实施回调** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **活动代码** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* **表示**操作失败。

* **实施回调** `onNotification(NotificationEvent event)`

* **活动代码** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* **含义**播放范围已更新。

* **实施回调** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **活动代码** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* **意味着**屏幕上会显示新的播放速率。

* **实施回调** `onRatePlaying(PlaybackRateEvent event)`

* **活动代码** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* **含义**已设置MediaPlayer的rate属性。

* **实施回调** `onRateSelected(PlaybackRateEvent event)`

* **活动代码** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* **含义**开始播放。

* **实施回调** `onPlayStart()`

* **活动代码** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* **含义** MediaPlayer的当前配置文件已更改。

* **实施回调** `onProfileChanged(ProfileEvent event)`

* **活动代码** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* **意思**播放到达时间轴保留。

* **实施回调** `onReservationReached(ReservationEvent event)`

* **活动代码** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* **含义**开始搜索操作。

* **实施回调** `onSeekBegin(SeekEvent event)`

* **活动代码** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* **含义**搜索操作已完成。

* **实施回调** `onSeekEnd(SeekEvent event)`

* **活动代码** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* **含义**由于内部播放规则或外部业务规则，搜索位置已被调整。

* **实施回调** `onPositionAdjusted(SeekEvent event)`

* **活动代码** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* **表示**介质大小可用。

* **实施回调** `onSizeAvailable(SizeAvailableEvent event)`

* **活动代码** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* **含义** MediaPlayer状态已更改。

* **实施回调** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **活动代码** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* **含义**播放头已更改。

* **实施回调** `onTimeChanged(TimeChangeEvent event)`

* **活动代码** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* **含义**此操作完成，并且所花费的时间为操作完成。

* **实施回调** `onTimedEvent(TimedEventEvent event)`

* **活动代码** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* **意味着**在后台向项目添加了新的定时元数据。

* **实施回调** `onTimedMetadata(TimedMetadataEvent event)`

* **活动代码** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* **含义**在媒体流中检测到新的定时元数据。

* **实施回调** `onTimedMetadata(TimedMetadataEvent event)`

* **活动代码** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* **含义**时间轴已修改。 广告可能已添加到时间轴中或从时间轴中删除。

* **实施回调** `onTimelineUpdated(TimelineEvent event)`

* **活动代码** `TIMELINE_UPDATED`