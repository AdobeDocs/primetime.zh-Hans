---
description: CustomRangeMetadata类标识VOD流标记、删除和替换中不同类型的时间范围。 对于这些自定义时间范围类型中的每一种类型，您都可以执行相应的操作，包括删除和替换广告内容。
title: 自定义时间范围操作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# 自定义时间范围操作{#custom-time-range-operations}

CustomRangeMetadata类标识VOD流中不同类型的时间范围：标记、删除和替换。 对于这些自定义时间范围类型中的每一种类型，您都可以执行相应的操作，包括删除和替换广告内容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

对于广告删除和替换，TVSDK使用以下&#x200B;*自定义时间范围操作*&#x200B;模式：

* **MARKT** 该模式在TVSDK的早期版本中被称为自定义广告标记。该模式标记已放入VOD流中的广告的开始和结束时间。 当流中存在类型为`MARK`的时间范围标记时，由`CustomMarkerOpportunityGenerator`生成`Mode.MARK`的初始位置，并由`CustomRangeResolver`解析。 不插入任何广告。

* **DELETEF** 或时 `DELETE` 间范围中，初始 `placementInformation` 类型 `Mode.DELETE` 由创建和解析 `CustomRangeResolver`。`DeleteRangeTimelineOperation` 定义要从时间轴中删除的范围，TVSDK使 `removeByLocalTime` 用Adobe视频引擎(AVE)API完成此操作。如果存在DELETE范围和Adobe Primetime广告决策元数据，则先删除这些范围，然后`AuditudeResolver`使用典型的Adobe Primetime广告决策工作流程解析广告。

* **在** REPLACEF或 `REPLACE` 时间范围中，将创建两 `placementInformations` 个初始值，一 `Mode.DELETE` 个和一个 `Mode.REPLACE`。`CustomRangeResolver` 先删除时间范围，然后将指 `AuditudeResolver` 定广告插入时 `replaceDuration` 间轴中。如果未指定`replaceDuration`，则服务器确定要插入的内容。

为支持这些自定义时间范围操作，TVSDK提供以下内容：

* 多个内容解析器

   流可以具有基于广告信令模式和广告元数据的多个内容解析器。 行为会随广告信令模式和广告元数据的不同组合而改变。
* 使用`CustomMarkerOpportunityGenerator`的多个初始机会。
* 新的广告信令模式，`CUSTOM_RANGES`。

   广告根据来自外部源（如JSON文件）的时间范围数据进行放置。