---
description: TVSDK中的这些更改支持广告删除和替换。
title: 广告删除和替换API更改
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 广告删除和替换API更改 {#ad-deletion-and-replacement-api-changes}

TVSDK中的这些更改支持广告删除和替换。

* `AdSignalingMode` 已添加 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  `extractAdSignalingMode()`  — 已设置 `AdSignalingMode.CUSTOM_RANGES` 如果替换范围在元数据中。

* `PlacementType` 已添加 `CUSTOM_RANGE` 类型。

* `PlacementMode`

   * 已添加 `DELETE` 模式。
   * 已添加 `MARK` 模式
   * 已添加 `FreeReplace` mode — 此模式具有持续时间，但为纯插入

* `TimeRange` 不再是 `final` 类

* 已添加 `ReplaceTimeRange()` 方法

  扩展 `TimeRange` 拥有 `replacementDuration` 属性。 对于MARK和DELETE案例， `replacementDuration` 为0。

* `TimeRangeCollection`

   * 已添加 `toReplaceMetadata()` 用于提取的实用程序函数 `timeRanges`.

   * 已修改以使用 `DELETE` 和 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已添加 `createCustomTimeRangesFrom()`  — 从JSON文件为MARK/REPLACE/DELETE用例创建元数据。
   * 已删除 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 已添加 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 已添加 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未更改）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 已添加 `CustomRangesOpportunityGenerator` 当元数据包含自定义范围时

   * `doRetrieveResolvers()`

      * 添加 `CustomRangeResolver` 当DELETE和REPLACE自定义范围在元数据中存在时为
      * 已移动 `CustomAdMarkerResolver` 提前 `AuditudeResolver`

* 已添加 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空 — 无更新、VOD
   * `doProcess()` 创建新类型的新投放位置 `Placement.Delete_Range`

   * 已添加 `CustomRangeOppotunityGenerator` 到生成器列表的顶部 `DefaultContentFactory`，因此会在广告插入之前处理删除范围。

   * 已添加 `createCustomRangeOpportunities` 创建所有机会

     MARK — 每个有效标记范围有一个机会 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.MARK`

     DELETE — 每个有效的删除范围都有一个机会 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`

     REPLACE — 每个有效替换范围有两个机会：

      1. 删除范围机会 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`.

      1. 的Primetime广告决策广告机会 `PlacementType.MID_ROLL` 或 `PlacementType.PRE_ROLL` 和 `PlacementMode.FREEREPLACE`

* 已添加 `CustomRangeResolver`：

   * `doCanResolve()` 返回 `true` 用于删除范围。

   * 已添加 `createDeleteRangeOperation()` 创建 `DeleteRange` 对于投放位置

* 已添加 `CustomRangeHelper`：

   * 用于提取Mark/Delete/Replace的通用实用程序类 `timeRanges` 并加以处理。
   * 已添加 `extractCustomRangesMetadata()`
   * 已添加 `extractCustomRanges()`
   * 已添加 `mergeRanges()`  — 解决冲突和子集/合并

* `MediaPlayerTimeline`:

   * &quot;>In `executeOperation()`，如果操作为 `DeleteRange`，在操作中添加了删除方法的调用

   * 在 `executeOperation()`，如果操作为 `NOPTimelineOperation` （空） `AdBreaks` （从服务器返回），添加了清除调用。

   * 已添加 `onDeleteRangeComplete()`
   * 已添加 `removeRange()`
   * 在 `adjustPlacement()`，用于 `PlacementMode.FREEREPLACE` 模式，清空了持续时间。 请求时需要更早的持续时间 `AdBreaks`，此时需要为零，才能进行纯插入。

* `VideoEngineTimeline` 已添加 `removeC3Ad()`  — 调用 `removeByLocalTime()` 用于删除范围

* `AdSignalingModeGenerator`

   * `doConfigure()`  — 如果未生成机会，则不解析
   * `createInitialOpportunity()`  — 不为生成初始机会 `AdSignalingMode.CUSTOM_RANGE`. 此 `CustomRangeOpportunityGenerator` 已涵盖此内容。

* `DeleteRange`

   * 扩展 `TimelineOperation`.
   * 创建者 `CustomRangeResolver` 用于删除和替换（替换的删除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5`  — 允许打包
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 此 `accepts()` 修改了方法，允许打包不同的放置类型（前卷、中卷、后卷）

* `AuditudeRequestHelper` 错误修复，以允许服务器覆盖广告参数

* `AuditudeResolver` 此 `canBePacked()` 方法已更改为允许打包

* `CustomAdResolver` 此 `timeRange` 已删除提取函数。 我们一次得到一个位置，然后将其转换为 `AdBreakPlacement timelineOperation`.
