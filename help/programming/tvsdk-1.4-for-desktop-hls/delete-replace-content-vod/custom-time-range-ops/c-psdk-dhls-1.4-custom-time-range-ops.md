---
description: TVSDK支持在VOD流中以编程方式删除和替换广告内容。
title: 自定义时间范围操作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 概述{#custom-time-range-operations-overview}

TVSDK支持在VOD流中以编程方式删除和替换广告内容。

删除和替换功能扩展了自定义广告标记功能。 自定义广告标记将主要内容的部分标记为与广告相关的内容句点。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

广告删除和替换是通过自定义标记实现的，这些标记标识VOD流中不同类型的时间范围：标记、删除和替换。 对于每个自定义时间范围，您都可以执行相关操作，包括删除或替换广告内容。

对于广告删除和替换，TVSDK包括以下&#x200B;*自定义时间范围操作*&#x200B;模式：

* MARK — 为标记区域调度`AdBreak`事件。 （在TVSDK的早期版本中，这称为`customAdMarker`。） 在此模式下不允许插入广告。

* DELETE — 对于此模式，应用程序使用`TimeRangeCollection`类定义C3广告删除的时间区域。 在此模式下允许插入广告。
* REPLACE — 在此模式下，应用程序用Adobe Primetime广告决策`AdBreak`替换`timeRange`。 发生C3广告删除的替换操作开始，在指定时间结束（比原始时间范围短或长）。

TVSDK提供`CustomRangesOpportunityGenerator`类，以生成MARK和DELETE范围的放置机会。 对于REPLACE模式，TVSDK为每个时间范围生成两个放置机会：

* `CustomRangeResolver`生成DELETE的放置机会
* `AuditudeAdResolver`为INSERT生成放置机会。