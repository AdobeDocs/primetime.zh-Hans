---
description: CustomRangeMetadata类标识VOD流标记、删除和替换中不同类型的时间范围。 对于这些自定义时间范围类型中的每种类型，您都可以执行相应的操作，包括删除和替换广告内容。
seo-description: CustomRangeMetadata类标识VOD流标记、删除和替换中不同类型的时间范围。 对于这些自定义时间范围类型中的每种类型，您都可以执行相应的操作，包括删除和替换广告内容。
seo-title: 自定义时间范围操作
title: 自定义时间范围操作
uuid: eadd4d8d-0e03-40ca-ae3b-eede82bf2df8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# 自定义时间范围操作{#custom-time-range-operations}

CustomRangeMetadata类标识VOD流中不同类型的时间范围：标记、删除和替换。 对于这些自定义时间范围类型中的每种类型，您都可以执行相应的操作，包括删除和替换广告内容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

对于广告删除和替换，TVSDK使用以下&#x200B;*自定义时间范围操作*&#x200B;模式：

* **MARKT** 其模式在TVSDK的先前版本中称为自定义广告标记。该模式标记已放入VOD流的广告的开始和结束时间。 当流中存在类型为`MARK`的时间范围标记时，由`CustomMarkerOpportunityGenerator`生成`Mode.MARK`的初始位置，并由`CustomRangeResolver`解析。 不插入任何广告。

* **DELETEF** 或时 `DELETE` 间范围，初始 `placementInformation` 类型 `Mode.DELETE` 由创建和解析 `CustomRangeResolver`。`DeleteRangeTimelineOperation` 定义要从时间轴中删除的范围，TVSDK `removeByLocalTime` 使用Adobe视频引擎(AVE)API完成此操作。如果存在DELETE范围和Adobe Primetime广告决策元数据，则先删除这些范围，然后`AuditudeResolver`使用典型的Adobe Primetime广告决策工作流解析广告。

* **在** REPLACEF `REPLACE` 或时间范围中，将创建 `placementInformations` 两个初始值，一 `Mode.DELETE` 个和一 `Mode.REPLACE`个。`CustomRangeResolver` 先删除时间范围，然后将指 `AuditudeResolver` 定时间范围的广告 `replaceDuration` 插入时间轴。如果未指定`replaceDuration`，则服务器确定要插入的内容。

为支持这些自定义时间范围操作，TVSDK提供以下内容：

* 多个内容解析器

   流可以基于广告信令模式和广告元数据具有多个内容解析器。 广告信号模式和广告元数据的不同组合会改变行为。
* 使用`CustomMarkerOpportunityGenerator`的多个初始机会。
* 新的广告信令模式，`CUSTOM_RANGES`。

   广告根据来自外部源（如JSON文件）的时间范围数据进行放置。