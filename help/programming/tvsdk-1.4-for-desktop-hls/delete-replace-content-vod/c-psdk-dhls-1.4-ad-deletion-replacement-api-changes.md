---
description: TVSDK中的这些更改支持删除和替换广告。
seo-description: TVSDK中的这些更改支持删除和替换广告。
seo-title: 广告删除和替换API更改
title: 广告删除和替换API更改
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# 广告删除和替换API更改{#ad-deletion-and-replacement-api-changes}

TVSDK中的这些更改支持删除和替换广告。

* `AdSignalingMode` 添加了 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  `extractAdSignalingMode()` -在元 `AdSignalingMode.CUSTOM_RANGES` 数据中设置替换范围。

* `PlacementType` 已添 `CUSTOM_RANGE` 加类型。

* `PlacementMode`

   * 添加了`DELETE`模式。
   * 添加了`MARK`模式
   * 添加了`FreeReplace`模式——此模式具有持续时间，但是纯插入

* `TimeRange` 不再是课 `final` 程

* 添加了`ReplaceTimeRange()`方法

   扩展`TimeRange`以具有`replacementDuration`属性。 对于MARK和DELETE情况，`replacementDuration`为0。

* `TimeRangeCollection`

   * 添加了`toReplaceMetadata()`实用程序函数以解压`timeRanges`。

   * 修改为与`DELETE`和`REPLACE`一起使用

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 添加了`createCustomTimeRangesFrom()` —— 从JSON文件为MARK/DELETE/REPLACE用例创建元数据。
   * 已删除`createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 添加了`CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 添加了`CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未更改）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 添加了`CustomRangesOpportunityGenerator`，用于元数据包含自定义范围时
   * `doRetrieveResolvers()`

      * 添加`CustomRangeResolver`，当元数据中存在DELETE和REPLACE自定义范围时
      * 已将`CustomAdMarkerResolver`移到`AuditudeResolver`之前


* 添加了`CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空——无更新、VOD
   * `doProcess()` 创建新类型的新放置  `Placement.Delete_Range`

   * 将`CustomRangeOppotunityGenerator`添加到`DefaultContentFactory`中生成器列表的顶部，因此在插入广告之前会处理删除范围。

   * 添加了`createCustomRangeOpportunities`以创建所有机会

      MARK —— 每个有效标记范围`PlacementType.CUSTOM_RANGE`和`PlacementMode.MARK`只有一个机会

      DELETE-每个有效删除范围`PlacementType.CUSTOM_RANGE`和`PlacementMode.DELETE`只有一个机会

      REPLACE —— 每个有效替换范围有两个机会：

      1. `PlacementType.CUSTOM_RANGE`和`PlacementMode.DELETE`的删除范围机会。

      1. `PlacementType.MID_ROLL`或`PlacementType.PRE_ROLL`和`PlacementMode.FREEREPLACE`的Primetime广告决策广告机会

* 添加了`CustomRangeResolver`:

   * `doCanResolve()` 返回 `true` 删除范围。

   * 添加了`createDeleteRangeOperation()`以创建放置的`DeleteRange`

* 添加了`CustomRangeHelper`:

   * 用于提取标记／删除／替换`timeRanges`并处理它们的公用程序类。
   * 添加了`extractCustomRangesMetadata()`
   * 添加了`extractCustomRanges()`
   * 添加了`mergeRanges()` —— 解决冲突和子集／合并

* `MediaPlayerTimeline`:

   * &quot;>在`executeOperation()`中，如果操作为`DeleteRange`，则在操作中添加了对remove方法的调用

   * 在`executeOperation()`中，如果操作为`NOPTimelineOperation`（从服务器返回的空`AdBreaks`），则添加了清除调用。

   * 添加了`onDeleteRangeComplete()`
   * 添加了`removeRange()`
   * 在`adjustPlacement()`模式下，将持续时间归零。 `PlacementMode.FREEREPLACE`在请求`AdBreaks`时，此持续时间较早，此时需要为零才能进行纯插入。

* `VideoEngineTimeline` 已添 `removeC3Ad()` 加——调 `removeByLocalTime()` 用删除范围

* `AdSignalingModeGenerator`

   * `doConfigure()` -如果未生成任何机会，则不解决
   * `createInitialOpportunity()` -不要为生成初始机会 `AdSignalingMode.CUSTOM_RANGE`。`CustomRangeOpportunityGenerator`已涵盖此问题。

* `DeleteRange`

   * 扩展`TimelineOperation`。
   * 由`CustomRangeResolver`创建，用于删除和替换（替换的删除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` -允许打包
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 修 `accepts()` 改了该方法，以允许不同放置类型（预卷、中卷、后卷）的包装

* `AuditudeRequestHelper` 允许服务器覆盖广告参数的错误修复

* `AuditudeResolver` 方 `canBePacked()` 法已更改，允许打包

* `CustomAdResolver` 已 `timeRange` 删除提取函数。我们一次只得到一个位置，然后将其转换为`AdBreakPlacement timelineOperation`。

