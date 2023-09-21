---
description: TVSDK支持以编程方式删除和替换VOD流中的广告内容。
title: 自定义时间范围操作
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 概述 {#custom-time-range-operations-overview}

TVSDK支持以编程方式删除和替换VOD流中的广告内容。

删除和替换功能可进一步扩展自定义广告标记功能。 自定义广告标记将主内容的各个部分标记为与广告相关的内容时段。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

使用可识别VOD流中不同类型的时间范围的自定义标记来实现广告删除和替换：标记、删除和替换。 对于每个自定义时间范围，您可以执行关联的操作，包括删除或替换广告内容。

对于广告删除和替换，TVSDK包括以下内容 *自定义时间范围操作* 模式：

* 标记 — 调度 `AdBreak` 标记区域的事件。 (这称为 `customAdMarker` （在TVSDK的早期版本中）。 在此模式下不允许广告插入。

* DELETE — 对于此模式，应用程序使用 `TimeRangeCollection` 类以定义C3广告删除的时间区域。 在此模式下允许广告插入。
* REPLACE — 在此模式下，应用程序将替换 `timeRange` 使用Adobe Primetime ad decisioning `AdBreak`. 替换操作从发生C3广告删除的位置开始，并在指定时间（比原始时间范围更短或更长）结束。

TVSDK提供 `CustomRangesOpportunityGenerator` 类为MARK和DELETE范围生成投放机会。 对于REPLACE模式，TVSDK会为每个时间范围生成两个放置机会：

* 此 `CustomRangeResolver` 为DELETE生成投放位置
* 此 `AuditudeAdResolver` 为INSERT生成放置机会。
