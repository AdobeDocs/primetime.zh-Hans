---
description: Android TVSDK API中的这些更改支持广告删除和替换。
title: 广告删除和替换API更改
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# 广告删除和替换API更改{#ad-deletion-and-replacement-api-changes}

Android TVSDK API中的这些更改支持广告删除和替换。

* `AdSignalingMode` 新的自定义时间范围和信令模式

* `AdvertisingMetadata` 新建 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`：设置处理元数据时标记、删除或替换的时间范围

* `ContentResolver`

   * 新建 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 新建 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 新建 `ContentRemoval` 类

  `TimelineOperation` 类定义要从时间轴中删除的时间范围

* `AuditudeResolver`

   * 新建 `private LinkedList<AuditudeRequest> _requestQueue`
   * 新建 `void startConsumer()`：开始处理Primetime ad decisioning请求队列，并确保在以下时间发出每个请求： `MIN_INIT_REQUEST_INTERVAL` 间隔

   * 新建 `processReplacementRange()`：从广告元数据中提取时间范围并生成 `PlacementInformations`，并创建一个Primetime广告决策请求，其中包含 `PlacementInformations`.

   * 新建 `canDoResolver()`：检查投放位置机会是否具有Primetime广告决策元数据

* 新建 `CustomRangeHelper` 从广告元数据中提取时间范围元数据并删除子集/重叠/无效时间范围的帮助程序类。

* 新建 `DeleteContentResolver` 解决投放机会的内容解析程序 `PlacementInformation.Mode.DELETE`

* 新建 `NopTimelineOperation` 新的时间线操作，适用于不需要执行广告时间放置或替换的情况。 此类用于区分这点以及在解析过程中何时发生错误。

* `TimelineOperationQueue` 检查时间线操作是否为 `NopTimelineOperation` 处理之前。

* `CustomAdMarkersContentResolver` 新建 `canDoResolve()`：检查投放位置机会是否属于类型 `Mode.MARK`

* `MetadataResolver` 新建 `canDoResolve()`：检查投放位置机会是否属于类型 `Mode.INSERT`

* `DefaultMetadataKeys` 新建 `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 新模式 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 新类型 `CUSTOM_TIME_RANGES`

* `TimeRange` 新建 `compareTo(TimeRange timeRange)`：因此，可以根据开始时间对时间范围进行排序

* 新建 `ReplacementTimeRange` 扩展 `TimeRange` 类表示替换时间范围，使用 `begin`， `end`、和 `replacement-duration` 参数。

* `TimeRangeCollection`

   * 新建 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 已重命名 `CUSTOM_AD_MARKERS` 到 `MARK_RANGES`

   * 修改时间 `toMetadata(Metadata options)` 将删除/标记/替换范围放入广告元数据。

* `MediaPlayerNotification`

   * 新建 `UNDEFINED_TIME_RANGES`：当广告信令模式为服务器映射或清单提示，并且替换范围也在广告元数据中时，替换范围被忽略。
   * 新建 `REPLACE_RANGES_NOT_AVAILABLE`：当广告信号模式为自定义时间范围并且替换范围不可用时，将发送警告。

* `AdvertisingFactory` 新建 `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 新建 `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 新建 `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 在 `prepareToPlay()`：对0进行初始搜寻，因为 `[0,n]` ，则媒体播放器不会自动播放。

   * 在 `prepareToPlay()`：在初始投放位置信息列表中循环 `mediaplayerclient` 以解决。

   * 在 `extractAdSignalingMode()`：适应新的自定义时间范围模式。
   * 新建 `private static List<PlacementInformation> createInitalPlacementInformations()`：为广告信令模式和内容解析器生成初始投放位置信息（派生自广告元数据）。
   * 在 `ContentPlacementCompletedListener`：检查以查看 `mediaPlayerClient` 是 `doneInitialResolving` 调用之前 `endAdResolving`.

* `MediaPlayerClient`

   * 新建 `List<ContentResolver> _contentResolvers`
   * 新建 `int _reservations`
   * 新建 `lookupContentResolver(PlacementOpportunity placementOpportunity)`：查找哪个解析程序可以解析 `PlacementOpportunity`.

   * 修改了用于创建多个内容解析器的代码。
   * 新建 `public boolean doneInitialResolving()`：检查是否存在任何未解决的机会。

* `VideoEngineTimeline`

   * 新建 `removeContent(TimelineOperation timelineOperation)`：从时间轴中删除给定的内容范围。
   * 新建 `removeContentByLocalTime(long begin, long end)`：按给定的本地时间删除内容 `begin` 和 `end`.

* `DefaultOpportunityDetectorFactory` 修改时间 `createOpportunityDetector`：对于VOD流，仅返回新的 `SpliceOutOpportunityDetector` 如果没有MARK或REPLACE范围（因为这些范围优先于信令模式）。
