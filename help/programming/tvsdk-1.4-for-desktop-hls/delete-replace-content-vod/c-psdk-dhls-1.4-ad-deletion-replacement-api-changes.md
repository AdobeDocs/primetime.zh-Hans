---
description: TVSDK中的这些更改支持广告删除和替换。
title: 广告删除和替换API更改
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 广告删除和替换API更改 {#ad-deletion-and-replacement-api-changes}

TVSDK中的这些更改支持广告删除和替换。

* `AdSignalingMode` 已添加 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  `extractAdSignalingMode()`  — 设置 `AdSignalingMode.CUSTOM_RANGES` 如果替换范围在元数据中。

* `PlacementType` 已添加 `CUSTOM_RANGE` 类型。

* `PlacementMode`

   * 已添加 `DELETE` 模式。
   * 已添加 `MARK` 模式
   * 已添加 `FreeReplace` mode — 此模式具有持续时间，但只是单纯的插入

* `TimeRange` 不再是 `final` 类

* 已添加 `ReplaceTimeRange()` 方法

   扩展 `TimeRange` 拥有 `replacementDuration` 属性。 对于MARK和DELETE案例， `replacementDuration` 为0。

* `TimeRangeCollection`

   * 已添加 `toReplaceMetadata()` 用于提取的实用程序函数 `timeRanges`.

   * 修改后可使用 `DELETE` 和 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已添加 `createCustomTimeRangesFrom()`  — 从JSON文件为MARK/REPLACE/REPLACE用例创建DELETE。
   * 已删除 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 已添加 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 已添加 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未更改）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 已添加 `CustomRangesOpportunityGenerator` 当元数据包含自定义范围时为
   * `doRetrieveResolvers()`

      * 添加 `CustomRangeResolver` 当DELETE和REPLACE自定义范围存在于元数据中时为
      * 已移动 `CustomAdMarkerResolver` 超前 `AuditudeResolver`


* 已添加 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空 — 无更新、VOD
   * `doProcess()` 创建新类型的新投放位置 `Placement.Delete_Range`

   * 已添加 `CustomRangeOppotunityGenerator` 到发电机列表顶端 `DefaultContentFactory`，因此在广告插入之前会处理删除范围。

   * 已添加 `createCustomRangeOpportunities` 创造所有机会

      MARK — 每个有效的标记范围有一个机会 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.MARK`

      DELETE — 每个有效的删除范围都有一个机会 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`

      REPLACE — 每个有效替换范围有两个机会：

      1. 删除范围机会 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`.

      1. Primetime广告决策广告机会 `PlacementType.MID_ROLL` 或 `PlacementType.PRE_ROLL` 和 `PlacementMode.FREEREPLACE`

* 已添加 `CustomRangeResolver`：

   * `doCanResolve()` 返回 `true` 用于删除范围。

   * 已添加 `createDeleteRangeOperation()` 创建 `DeleteRange` 用于投放

* 已添加 `CustomRangeHelper`：

   * 用于提取Mark/Delete/Replace的公用实用程序类 `timeRanges` 并加以处理。
   * 已添加 `extractCustomRangesMetadata()`
   * 已添加 `extractCustomRanges()`
   * 已添加 `mergeRanges()`  — 解决冲突和子集/合并

* `MediaPlayerTimeline`:

   * “>In `executeOperation()`，如果操作为 `DeleteRange`，在操作中添加了删除方法的调用

   * In `executeOperation()`，如果操作为 `NOPTimelineOperation` （空） `AdBreaks` （从服务器返回），添加了要清除的调用。

   * 已添加 `onDeleteRangeComplete()`
   * 已添加 `removeRange()`
   * In `adjustPlacement()`，表示 `PlacementMode.FREEREPLACE` 模式，清空了持续时间。 在请求时，需要更早的持续时间 `AdBreaks`，此时，它需要为零，才能为纯插入。

* `VideoEngineTimeline` 已添加 `removeC3Ad()`  — 调用 `removeByLocalTime()` 用于删除范围

* `AdSignalingModeGenerator`

   * `doConfigure()`  — 如果未生成机会，则不解析
   * `createInitialOpportunity()`  — 不为生成初始机会 `AdSignalingMode.CUSTOM_RANGE`. 此 `CustomRangeOpportunityGenerator` 已涵盖此内容。

* `DeleteRange`

   * 扩展 `TimelineOperation`.
   * 创建者 `CustomRangeResolver` 删除和替换（替换的删除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5`  — 允许打包
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 此 `accepts()` 修改了方法，以便能够打包不同的放置类型（前段、中段、后段）

* `AuditudeRequestHelper` 允许服务器覆盖Ad参数的错误修复

* `AuditudeResolver` 此 `canBePacked()` 方法已更改为允许打包

* `CustomAdResolver` 此 `timeRange` 已删除提取函数。 我们每次得到一个位置，然后将其转换为 `AdBreakPlacement timelineOperation`.
