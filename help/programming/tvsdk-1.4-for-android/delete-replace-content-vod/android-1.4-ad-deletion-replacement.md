---
description: Android TVSDK API中的这些更改支持和删除和替换。
seo-description: Android TVSDK API中的这些更改支持和删除和替换。
seo-title: 广告删除和替换API更改
title: 广告删除和替换API更改
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 广告删除和替换API更改{#ad-deletion-and-replacement-api-changes}

Android TVSDK API中的这些更改支持和删除和替换。

* `AdSignalingMode` 新的自定义时间范围广告信令模式

* `AdvertisingMetadata` 新增功 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`能：设置处理元数据时要标记、删除或替换的时间范围

* `ContentResolver`

   * 新增功能 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 新增功能 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 新课 `ContentRemoval` 程

   `TimelineOperation` 定义要从时间轴中删除的时间范围的类

* `AuditudeResolver`

   * 新增功能 `private LinkedList<AuditudeRequest> _requestQueue`
   * 新增功 `void startConsumer()`能：开始处理Primetime广告决策请求队列并确保每个请求按时间间隔发 `MIN_INIT_REQUEST_INTERVAL` 出

   * 新增功 `processReplacementRange()`能：从广告元数据中提取时间范围并生成 `PlacementInformations`，并创建包含该元数据的Primetime广告决策请求 `PlacementInformations`。

   * 新增功 `canDoResolver()`能：检查放置机会是否包含Primetime广告决策元数据

* 新的 `CustomRangeHelper` 帮助程序类从广告元数据中提取时间范围元数据，并删除子集／重叠／无效时间范围。

* 新的 `DeleteContentResolver` 内容解析程序解决了 `PlacementInformation.Mode.DELETE`

* 新的 `NopTimelineOperation` 新时间轴操作，用于无需进行广告中断投放或替换的时间。 此类用于区分此类和解析过程中何时出错。

* `TimelineOperationQueue` 在处理之前检查时间轴操作 `NopTimelineOperation` 是否为。

* `CustomAdMarkersContentResolver` 新增功 `canDoResolve()`能：检查职位安排机会的类型 `Mode.MARK`

* `MetadataResolver` 新增功 `canDoResolve()`能：检查职位安排机会的类型 `Mode.INSERT`

* `DefaultMetadataKeys` 新增功能 `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 新模式 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 新类型 `CUSTOM_TIME_RANGES`

* `TimeRange` 新增功 `compareTo(TimeRange timeRange)`能：因此，可以根据开始时间对TimeRanges进行排序

* 新增 `ReplacementTimeRange` 功能扩展 `TimeRange` 了表示替换时间范围的类，该类包含 `begin`、 `end`和 `replacement-duration` 参数。

* `TimeRangeCollection`

   * 新增功能 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 已重命 `CUSTOM_AD_MARKERS` 名为 `MARK_RANGES`

   * 已修 `toMetadata(Metadata options)` 改以将删除／标记／替换范围放入广告元数据中。

* `MediaPlayerNotification`

   * 新增功 `UNDEFINED_TIME_RANGES`能：当广告信令模式是服务器映射或清单提示时，替换范围也在广告元数据中时，替换范围将被忽略。
   * 新增功 `REPLACE_RANGES_NOT_AVAILABLE`能：当广告信令模式为自定义时间范围且替换范围不可用时，将调度警告。

* `AdvertisingFactory` 新增功能 `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 新增功能 `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 新增功能 `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 在 `prepareToPlay()`:对0进行初始搜索，因为如果删 `[0,n]` 除范围，媒体播放器不会自动播放。

   * 在 `prepareToPlay()`:循环浏览要解析的初始放置信 `mediaplayerclient` 息列表。

   * 在 `extractAdSignalingMode()`:适应新的“自定义时间范围”模式。
   * 新增功 `private static List<PlacementInformation> createInitalPlacementInformations()`能：为广告信令模式和内容解析器（从广告元数据派生）生成初始放置信息。
   * 在 `ContentPlacementCompletedListener`:在拔打电话前检 `mediaPlayerClient` 查 `doneInitialResolving` 是否是 `endAdResolving`。

* `MediaPlayerClient`

   * 新增功能 `List<ContentResolver> _contentResolvers`
   * 新增功能 `int _reservations`
   * 新增功 `lookupContentResolver(PlacementOpportunity placementOpportunity)`能：查找可解析程序的解析程 `PlacementOpportunity`序。

   * 修改了用于创建多个内容解析器的代码。
   * 新增功 `public boolean doneInitialResolving()`能：检查是否还有待解决的机会。

* `VideoEngineTimeline`

   * 新增功 `removeContent(TimelineOperation timelineOperation)`能：从时间轴中删除给定范围的内容。
   * 新增功 `removeContentByLocalTime(long begin, long end)`能：按给定和的本地时间删除 `begin` 内容 `end`。

* `DefaultOpportunityDetectorFactory` 修改时 `createOpportunityDetector`间：对于VOD流，只有在没有MARK或REPLACE `SpliceOutOpportunityDetector` 范围时（因为这些范围优先于信令模式）才返回新的。

