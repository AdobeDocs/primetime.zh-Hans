---
description: CustomRangeMetadata类标识VOD流标记、删除和替换中不同类型的时间范围。 对于每种自定义时间范围类型，您可以执行相应的操作，包括删除和替换广告内容。
title: 自定义时间范围操作
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 概述 {#custom-time-range-operations}

CustomRangeMetadata类标识VOD流中不同类型的时间范围：标记、删除和替换。 对于每种自定义时间范围类型，您可以执行相应的操作，包括删除和替换广告内容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

对于广告删除和替换，TVSDK使用以下对象 *自定义时间范围操作* 模式：

* **标记** 此模式在TVSDK的早期版本中称为自定义广告标记。 模式会标记已置于VOD流中的广告的开始和结束时间。 当存在类型为的时间范围标记时 `MARK` 在流中，初始投放位置为 `Mode.MARK` 生成者 `CustomMarkerOpportunityGenerator` 解决者 `CustomRangeResolver`. 未插入广告。

* **DELETE** 对象 `DELETE` 时间范围，初始 `placementInformation` 类型 `Mode.DELETE` 创建者和解决者 `CustomRangeResolver`. `DeleteRangeTimelineOperation` 定义要从时间轴中删除的范围，TVSDK将使用 `removeByLocalTime` 从Adobe视频引擎(AVE) API完成此操作。 如果存在DELETE范围和Adobe Primetime ad decisioning元数据，则会先删除这些范围，然后 `AuditudeResolver` 使用典型的Adobe Primetime ad decisioning工作流解析广告。

* **REPLACE** 对象 `REPLACE` 时间范围，两个初始值 `placementInformations` 创建一个 `Mode.DELETE` 和一个 `Mode.REPLACE`. `CustomRangeResolver` 先删除时间范围，然后 `AuditudeResolver` 插入指定内容的广告 `replaceDuration` 放到时间线中。 如果否 `replaceDuration` 指定时，服务器将确定要插入的内容。

为了支持这些自定义时间范围操作，TVSDK提供了以下功能：

* 多个内容解析器

  一个流可以具有多个基于广告信令模式和广告元数据的内容解析器。 广告信令模式和广告元数据的不同组合会改变广告的行为。
* 多个初始机会，使用 `CustomMarkerOpportunityGenerator`.
* 新的广告信号模式， `CUSTOM_RANGES`.

  广告投放基于来自外部源的时间范围数据，如JSON文件。
