---
description: Android TVSDK API中的这些更改支持删除和替换。
title: 广告删除和替换API更改
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# 广告删除和替换API更改{#ad-deletion-and-replacement-api-changes}

Android TVSDK API中的这些更改支持删除和替换。

* `AdSignalingMode` 新的自定义时间范围广告信令模式

* `AdvertisingMetadata` 新增功 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`能：设置处理元数据时要标记、删除或替换的时间范围

* `ContentResolver`

   * 新`public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 新`protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 新建`ContentRemoval`类

   `TimelineOperation` 定义要从时间轴中删除的时间范围的类

* `AuditudeResolver`

   * 新`private LinkedList<AuditudeRequest> _requestQueue`
   * 新`void startConsumer()`:开始处理Primetime广告决策请求队列并确保每个请求按`MIN_INIT_REQUEST_INTERVAL`时间间隔发出

   * 新`processReplacementRange()`:从广告元数据提取时间范围并生成`PlacementInformations`，并创建包含`PlacementInformations`的Primetime广告决策请求。

   * 新`canDoResolver()`:检查放置机会是否包含Primetime广告决策元数据

* 新的`CustomRangeHelper`帮助程序类从广告元数据中提取时间范围元数据，并删除子集/重叠/无效的时间范围。

* 新的`DeleteContentResolver`内容解析程序，可解决`PlacementInformation.Mode.DELETE`的放置机会

* 新`NopTimelineOperation`新时间轴操作，用于无需放置或替换广告时。 此类用于区分此类和解析过程中发生错误时。

* `TimelineOperationQueue` 在处理之前检查时间轴操 `NopTimelineOperation` 作是否为。

* `CustomAdMarkersContentResolver` 新增功 `canDoResolve()`能：检查放置机会是否为类型  `Mode.MARK`

* `MetadataResolver` 新增功 `canDoResolve()`能：检查放置机会是否为类型  `Mode.INSERT`

* `DefaultMetadataKeys` 新增  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 新模式`enum (INSERT, DELETE, REPLACE, MARK)`
   * 新类型`CUSTOM_TIME_RANGES`

* `TimeRange` 新增功 `compareTo(TimeRange timeRange)`能：因此，可以根据开始时间对时间范围进行排序

* 新`ReplacementTimeRange`扩展表示替换时间范围的`TimeRange`类，该类具有`begin`、`end`和`replacement-duration`参数。

* `TimeRangeCollection`

   * 新`MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 将`CUSTOM_AD_MARKERS`重命名为`MARK_RANGES`

   * 已修改`toMetadata(Metadata options)`以将删除/标记/替换范围放入广告元数据中。

* `MediaPlayerNotification`

   * 新`UNDEFINED_TIME_RANGES`:当广告信令模式是服务器映射或清单提示，并且替换范围也在广告元数据中时，将忽略替换范围。
   * 新`REPLACE_RANGES_NOT_AVAILABLE`:当广告信令模式为自定义时间范围且替换范围不可用时，将发出警告。

* `AdvertisingFactory` 新增  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 新增  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 新增  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 在`prepareToPlay()`中：将初始搜索设置为0，因为如果删除范围`[0,n]`，媒体播放器将不会自动播放。

   * 在`prepareToPlay()`中：循环列表初始放置信息，以便`mediaplayerclient`解析。

   * 在`extractAdSignalingMode()`中：适应新的“自定义时间范围”模式。
   * 新`private static List<PlacementInformation> createInitalPlacementInformations()`:为广告信令模式和内容解析器（从广告元数据派生）生成初始放置信息。
   * 在`ContentPlacementCompletedListener`中：在调用`endAdResolving`之前检查`mediaPlayerClient`是否为`doneInitialResolving`。

* `MediaPlayerClient`

   * 新`List<ContentResolver> _contentResolvers`
   * 新`int _reservations`
   * 新`lookupContentResolver(PlacementOpportunity placementOpportunity)`:查找哪个解析程序可以解析`PlacementOpportunity`。

   * 修改代码以创建多个内容解析器。
   * 新`public boolean doneInitialResolving()`:检查是否还有待解决的机会。

* `VideoEngineTimeline`

   * 新`removeContent(TimelineOperation timelineOperation)`:从时间轴中删除给定范围的内容。
   * 新`removeContentByLocalTime(long begin, long end)`:按给定`begin`和`end`的本地时间删除内容。

* `DefaultOpportunityDetectorFactory` 已修 `createOpportunityDetector`改：对于VOD流，仅在没有MARK或REPLACE `SpliceOutOpportunityDetector` 范围时返回新值（因为这些范围比信令模式具有优先级）。

