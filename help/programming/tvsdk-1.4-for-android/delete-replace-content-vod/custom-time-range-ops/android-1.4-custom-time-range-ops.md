---
description: TVSDK支持程序化删除和替换VOD流中的广告内容。
seo-description: TVSDK支持程序化删除和替换VOD流中的广告内容。
seo-title: 自定义时间范围操作
title: 自定义时间范围操作
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 自定义时间范围操作 {#custom-time-range-operations}

TVSDK支持程序化删除和替换VOD流中的广告内容。

删除和替换功能扩展了自定义广告标记功能。 自定义广告标记将主要内容的部分标记为与广告相关的内容句点。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

广告删除和替换是通过标识 `TimeRange` VOD流中不同类型时间范围的元素实现的：标记、删除和替换。 对于这些自定义时间范围类型中的每种类型，您可以执行相应的操作，包括删除和替换广告内容。

对于广告删除和替换，TVSDK使用以下自定 *义时间范围操作模* 式：

* **MARK**（在TVSDK的早期版本中，这些标记称为自定义广告标记）。 它们标记已放入VOD流中的广告的开始和结束时间。 当流中存在MARK类型的时间范围标记时，由生成并解 `Mode.MARK` 析初始放置的位置 `CustomAdMarkersContentResolver`。 不插入广告。

* **删除**&#x200B;对于删除时间范围，将创建一个初 `placementInformation` 始类型 `Mode.DELETE` 并由相应的时间解析该类型 `DeleteContentResolver`。 `ContentRemoval` 是定义 `timelineOperation` 要从时间轴中删除的范围的新增功能。 TVSDK使 `removeByLocalTime` 用Adobe Video Engine(AVE)API来促进该操作。 如果存在DELETE范围和Adobe Primetime广告决策（以前称为Auditude）元数据，则先删除这些范围，然后使用常规的Adobe Primetime广告决策工作流程解析 `AuditudeResolver` 广告。

* **REPLACE**&#x200B;对于REPLACE时间范围，将创建两个 `placementInformations` 初始值，一个 `Mode.DELETE` 和一个 `Mode.REPLACE`。 先 `DeleteContentResolver` 删除时间范围，然后将指定 `AuditudeResolver` 的广告插入时间 `replaceDuration` 轴中。 如果未 `replaceDuration` 指定，则服务器确定要插入的内容。

为支持这些自定义时间范围操作，TVSDK提供以下内容：

* 多个内容解析器

   基于广告信令模式和广告元数据的流可以具有多个内容解析器。 行为会随着广告信令模式和广告元数据的不同组合而发生变化。
* 多个初 `PlacementInformations` 始根 `DefaultMediaPlayer` 据广告信令模式 `PlacementInformations` 和要由该解析的广告元数据创建初始列表 `MediaPlayerClient`。

* 新的广告信令模式：自定义时间范围

   广告根据来自外部源（如JSON文件）的时间范围数据进行放置。