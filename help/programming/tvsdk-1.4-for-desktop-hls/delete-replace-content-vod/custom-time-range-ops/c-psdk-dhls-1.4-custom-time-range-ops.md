---
description: TVSDK支持程序化删除和替换VOD流中的广告内容。
seo-description: TVSDK支持程序化删除和替换VOD流中的广告内容。
seo-title: 自定义时间范围操作
title: 自定义时间范围操作
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概述 {#custom-time-range-operations-overview}

TVSDK支持程序化删除和替换VOD流中的广告内容。

删除和替换功能扩展了自定义广告标记功能。 自定义广告标记将主要内容的部分标记为与广告相关的内容句点。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

广告删除和替换是使用自定义标记实现的，这些标记标识VOD流中不同类型的时间范围：标记、删除和替换。 对于每个自定义时间范围，您都可以执行相关操作，包括删除或替换广告内容。

对于广告删除和替换，TVSDK包括以下自定 *义时间范围操作模* 式：

* MARK —— 为标记 `AdBreak` 的区域分派事件。 (在TVSDK的 `customAdMarker` 早期版本中调用了此。)在此模式下不允许广告插入。

* 删除——对于此模式，应用程序使用类 `TimeRangeCollection` 定义C3广告删除的时间区域。 此模式允许广告插入。
* 替换——在此模式下，应用程序将用Adobe Primetime `timeRange` 广告决策替换广告决策 `AdBreak`。 替换操作从C3广告删除发生的位置开始，并在指示的时间（比原始时间范围短或长）结束。

TVSDK提供一个 `CustomRangesOpportunityGenerator` 类，用于为MARK和DELETE范围生成放置机会。 对于REPLACE模式，TVSDK会为每个时间范围生成两个位置机会：

* 生成 `CustomRangeResolver` DELETE的放置机会
* 为插 `AuditudeAdResolver` 入生成放置机会。