---
description: TVSDK支持程序化删除和替换VOD流中的广告内容。
seo-description: TVSDK支持程序化删除和替换VOD流中的广告内容。
seo-title: 自定义时间范围操作
title: 自定义时间范围操作
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 概述{#custom-time-range-operations-overview}

TVSDK支持程序化删除和替换VOD流中的广告内容。

删除和替换功能扩展了自定义广告标记功能。 自定义广告标记将主内容的各个部分标记为与广告相关的内容句点。 除了标记这些时间范围外，您还可以删除和替换时间范围。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

广告删除和替换是通过自定义标记实现的，这些标记标识VOD流中不同类型的时间范围：标记、删除和替换。 对于每个自定义时间范围，您可以执行相关操作，包括删除或替换广告内容。

对于广告删除和替换，TVSDK包括以下&#x200B;*自定义时间范围操作*&#x200B;模式：

* MARK —— 为标记区域分派`AdBreak`事件。 （在以前版本的TVSDK中称为`customAdMarker`。） 此模式不允许广告插入。

* DELETE-对于此模式，应用程序使用`TimeRangeCollection`类定义C3广告删除的时间区域。 在此模式下允许广告插入。
* REPLACE —— 在此模式下，应用程序将`timeRange`替换为Adobe Primetime广告决策`AdBreak`。 发生C3广告删除的替换操作开始，在指定时间结束（比原始时间范围短或长）。

TVSDK提供`CustomRangesOpportunityGenerator`类，为MARK和DELETE范围生成放置机会。 对于REPLACE模式，TVSDK为每个时间范围生成两个位置机会：

* `CustomRangeResolver`为DELETE生成位置机会
* `AuditudeAdResolver`为INSERT生成放置机会。