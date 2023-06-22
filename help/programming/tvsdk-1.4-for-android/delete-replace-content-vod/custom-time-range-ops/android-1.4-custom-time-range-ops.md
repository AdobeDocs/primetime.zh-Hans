---
description: TVSDK支持以编程方式删除和替换VOD流中的广告内容。
title: 自定义时间范围操作
exl-id: 10aa3609-d5d0-49e2-959f-d72d8dbd6ef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 自定义时间范围操作 {#custom-time-range-operations}

TVSDK支持以编程方式删除和替换VOD流中的广告内容。

删除和替换功能会扩展自定义广告标记功能。 自定义广告标记将主要内容的部分标记为与广告相关的内容时段。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

使用实施广告删除和替换 `TimeRange` 标识VOD流中不同类型时间范围的元素：标记、删除和替换。 对于每种自定义时间范围类型，您可以执行相应的操作，包括删除和替换广告内容。

对于广告删除和替换，TVSDK使用以下功能 *自定义时间范围操作* 模式：

* **标记**
（在TVSDK的早期版本中，这些标记称为自定义广告标记）。 它们标记已置于VOD流中的广告的开始和结束时间。 当流中有MARK类型的时间范围标记时，初始放置 
`Mode.MARK` 由生成并解析 `CustomAdMarkersContentResolver`. 未插入广告。

* **DELETE**
对于DELETE时间范围，使用初始 
`placementInformation` 类型 `Mode.DELETE` 由相应的创建和解析 `DeleteContentResolver`. `ContentRemoval` 是新的 `timelineOperation` 定义要从时间轴中删除的范围。 TVSDK使用 `removeByLocalTime` 从Adobe视频引擎(AVE) API访问，以便执行该操作。 如果存在DELETE范围和Adobe Primetime ad decisioning（以前称为Auditude）元数据，则会先删除这些范围，然后再删除 `AuditudeResolver` 使用普通的Adobe Primetime广告决策工作流解析广告。

* **REPLACE**
对于REPLACE时间范围，使用两个初始值 
`placementInformations` 已创建，一个 `Mode.DELETE` 和一个 `Mode.REPLACE`. 此 `DeleteContentResolver` 先删除时间范围，然后 `AuditudeResolver` 插入指定内容的广告 `replaceDuration` 放入时间轴。 如果否 `replaceDuration` 指定时，服务器会确定要插入的内容。

为了支持这些自定义时间范围操作，TVSDK提供了以下功能：

* 多个内容解析器

   一个流可以具有多个基于广告信令模式和广告元数据的内容解析器。 该行为随广告信令模式和广告元数据的不同组合而变化。
* 多个初始 `PlacementInformations` 此 `DefaultMediaPlayer` 创建初始值列表 `PlacementInformations` 基于广告信令模式和广告元数据由 `MediaPlayerClient`.

* 新广告信号模式：自定义时间范围

   广告是根据来自外部源（如JSON文件）的时间范围数据投放的。
