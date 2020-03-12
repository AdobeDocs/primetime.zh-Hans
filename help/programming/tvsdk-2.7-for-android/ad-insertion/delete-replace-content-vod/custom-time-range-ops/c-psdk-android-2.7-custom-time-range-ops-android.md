---
description: CustomRangeMetadata类标识VOD流标记、删除和替换中的不同类型的时间范围。 对于这些自定义时间范围类型中的每种类型，您可以执行相应的操作，包括删除和替换广告内容。
seo-description: CustomRangeMetadata类标识VOD流标记、删除和替换中的不同类型的时间范围。 对于这些自定义时间范围类型中的每种类型，您可以执行相应的操作，包括删除和替换广告内容。
seo-title: 自定义时间范围操作
title: 自定义时间范围操作
uuid: e9c6a135-124e-44d4-adf2-dc9d671e2483
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 概述 {#custom-time-range-operations}

CustomRangeMetadata类标识VOD流中不同类型的时间范围：标记、删除和替换。 对于这些自定义时间范围类型中的每种类型，您可以执行相应的操作，包括删除和替换广告内容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

对于广告删除和替换，TVSDK使用以下自定 *义时间范围操作模* 式：

* **MARK** This mode is as custom ad markers in verious versions of TVSDK. 该模式标记已放入VOD流中的广告的开始和结束时间。 当流中存在类型的时间范 `MARK` 围标记时，由生成并 `Mode.MARK` 由解 `CustomMarkerOpportunityGenerator` 析初始位置 `CustomRangeResolver`。 不插入广告。

* **删除** 对于时 `DELETE` 间范围，初始类型 `placementInformation` 由创建 `Mode.DELETE` 并解析 `CustomRangeResolver`。 `DeleteRangeTimelineOperation` 定义要从时间轴中删除的范围，TVSDK使 `removeByLocalTime` 用Adobe视频引擎(AVE)API完成此操作。 如果存在DELETE范围和Adobe Primetime广告决策元数据，则先删除这些范围，然后使用典型的Adobe Primetime广告决策 `AuditudeResolver` 工作流程解析广告。

* **替换** 对于时 `REPLACE` 间范围，将创建两个初始 `placementInformations` 值，一个 `Mode.DELETE` 和一个 `Mode.REPLACE`。 `CustomRangeResolver` 先删除时间范围，然后将指 `AuditudeResolver` 定时间范围的广告插入 `replaceDuration` 时间轴中。 如果未 `replaceDuration` 指定，则服务器确定要插入的内容。

为支持这些自定义时间范围操作，TVSDK提供以下内容：

* 多个内容解析器

   基于广告信令模式和广告元数据的流可以具有多个内容解析器。 行为会随着广告信令模式和广告元数据的不同组合而发生变化。
* 使用Adobe Cloud的多个初始机会 `CustomMarkerOpportunityGenerator`。
* 新的广告信令模式， `CUSTOM_RANGES`。

   广告根据外部源（如JSON文件）的“时间范围”数据进行放置。

