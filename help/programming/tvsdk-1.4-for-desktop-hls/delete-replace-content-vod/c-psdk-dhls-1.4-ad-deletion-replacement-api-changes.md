---
description: TVSDK中的这些更改支持删除和替换。
seo-description: TVSDK中的这些更改支持删除和替换。
seo-title: 广告删除和替换API更改
title: 广告删除和替换API更改
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 广告删除和替换API更改 {#ad-deletion-and-replacement-api-changes}

TVSDK中的这些更改支持删除和替换。

* `AdSignalingMode` 添加了 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  -如 `extractAdSignalingMode()` 果替 `AdSignalingMode.CUSTOM_RANGES` 换范围在元数据中，则进行设置。

* `PlacementType` 已添加 `CUSTOM_RANGE` 类型。

* `PlacementMode`

   * 添加了 `DELETE` 模式。
   * 已添加模 `MARK` 式
   * 添加 `FreeReplace` 模式——此模式具有持续时间，但是纯粹的插入

* `TimeRange` 不再是类 `final` 别

* 添加的方 `ReplaceTimeRange()` 法

   扩展 `TimeRange` 为具有属 `replacementDuration` 性。 对于MARK和DELETE情况， `replacementDuration` 为0。

* `TimeRangeCollection`

   * 添加了 `toReplaceMetadata()` 用于提取的实用程序函 `timeRanges`数。

   * 修改为使用 `DELETE` 和 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已添 `createCustomTimeRangesFrom()` 加——从JSON文件为MARK/DELETE/REPLACE用例创建元数据。
   * 已删除 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 已添加 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 已添加 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未更改）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 为元 `CustomRangesOpportunityGenerator` 数据包含自定义范围时添加
   * `doRetrieveResolvers()`

      * 当元 `CustomRangeResolver` 数据中存在DELETE和REPLACE自定义范围时，添加
      * 领先 `CustomAdMarkerResolver` 于 `AuditudeResolver`


* 已添加 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空——无更新、VOD
   * `doProcess()` 创建新类型的新位置 `Placement.Delete_Range`

   * 已添 `CustomRangeOppotunityGenerator` 加到中的生成器列表顶部，因此 `DefaultContentFactory`删除范围会在广告插入之前进行处理。

   * 添加了 `createCustomRangeOpportunities` 用于创造所有机会的功能

      MARK —— 每个有效的标记范围和 `PlacementType.CUSTOM_RANGE``PlacementMode.MARK`

      删除——每个有效的删除范围和 `PlacementType.CUSTOM_RANGE``PlacementMode.DELETE`

      REPLACE —— 每个有效替换范围有两个机会：

      1. 和的删除范围 `PlacementType.CUSTOM_RANGE` 机会 `PlacementMode.DELETE`。

      1. Primetime广告决策广告机 `PlacementType.MID_ROLL` 会 `PlacementType.PRE_ROLL` 或 `PlacementMode.FREEREPLACE`

* 添加 `CustomRangeResolver`了：

   * `doCanResolve()` 返回 `true` 删除范围。

   * 已添 `createDeleteRangeOperation()` 加用于 `DeleteRange` 创建版面的内容

* 添加 `CustomRangeHelper`了：

   * 用于提取标记／删除／替换并处理这些标记的常 `timeRanges` 用实用程序类。
   * 已添加 `extractCustomRangesMetadata()`
   * 已添加 `extractCustomRanges()`
   * 添加 `mergeRanges()` 的——解决冲突和子集／合并

* `MediaPlayerTimeline`:

   * &quot;>在中， `executeOperation()`如果操作是，则在操 `DeleteRange`作中添加了对remove方法的调用

   * 在中， `executeOperation()`如果操作为(从服 `NOPTimelineOperation` 务器返 `AdBreaks` 回的空)，则添加了清除调用。

   * 已添加 `onDeleteRangeComplete()`
   * 已添加 `removeRange()`
   * 在模 `adjustPlacement()`式中， `PlacementMode.FREEREPLACE` 将持续时间设为零。 此持续时间在请求时较早 `AdBreaks`时需要，此时需要为零才能纯插入。

* `VideoEngineTimeline` 已添 `removeC3Ad()` 加——调 `removeByLocalTime()` 用删除范围

* `AdSignalingModeGenerator`

   * `doConfigure()` -如果未生成任何机会，请勿解决
   * `createInitialOpportunity()` -请勿为生成初始机会 `AdSignalingMode.CUSTOM_RANGE`。 这 `CustomRangeOpportunityGenerator` 个已经盖过了。

* `DeleteRange`

   * 扩展 `TimelineOperation`。
   * 由删除 `CustomRangeResolver` 和替换创建（替换的删除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` -允许打包
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 修 `accepts()` 改了该方法，以允许不同的铺放类型（预卷、中卷、后卷）的包装

* `AuditudeRequestHelper` 允许服务器覆盖广告参数的错误修复

* `AuditudeResolver` 方 `canBePacked()` 法已更改，允许包装

* `CustomAdResolver` 提取 `timeRange` 功能已被删除。 我们一次只得到一个职位，然后把它变成一个 `AdBreakPlacement timelineOperation`。

