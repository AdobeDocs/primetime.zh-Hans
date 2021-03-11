---
description: TVSDK支持在VOD流中以编程方式删除和替换广告内容。
title: 自定义时间范围操作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# 自定义时间范围操作{#custom-time-range-operations}

TVSDK支持在VOD流中以编程方式删除和替换广告内容。

删除和替换功能扩展了自定义广告标记功能。 自定义广告标记将主要内容的部分标记为与广告相关的内容句点。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

广告删除和替换是通过`TimeRange`元素实现的，这些元素标识VOD流中不同类型的时间范围：标记、删除和替换。 对于这些自定义时间范围类型中的每一种类型，您都可以执行相应的操作，包括删除和替换广告内容。

对于广告删除和替换，TVSDK使用以下&#x200B;*自定义时间范围操作*&#x200B;模式：

* **MARK**
（在TVSDK的早期版本中，这些标记称为自定义广告标记）。它们标记已放入VOD流中的广告的开始和结束时间。 当流中存在MARK类型的时间范围标记时， 
`Mode.MARK` 由生成和解析 `CustomAdMarkersContentResolver`。不插入任何广告。

* **DELETEF**
或DELETE时间范围，初始 
`placementInformation` 类型 `Mode.DELETE` 由相应的创建和解析 `DeleteContentResolver``ContentRemoval` 是定义 `timelineOperation` 要从时间轴中删除的范围的新增。TVSDK使用Adobe视频引擎(AVE)API中的`removeByLocalTime`来促进该操作。 如果存在DELETE范围和Adobe Primetime广告决策（以前称为Auditude）元数据，则先删除这些范围，然后`AuditudeResolver`使用普通的Adobe Primetime广告决策工作流解析广告。

* **REPLACEF或**
REPLACE时间范围，两个初始 
`placementInformations` ，一 `Mode.DELETE` 个 `Mode.REPLACE`。`DeleteContentResolver`首先删除时间范围，然后`AuditudeResolver`将指定`replaceDuration`的广告插入时间轴。 如果未指定`replaceDuration`，则服务器确定要插入的内容。

为支持这些自定义时间范围操作，TVSDK提供以下内容：

* 多个内容解析器

   流可以具有基于广告信令模式和广告元数据的多个内容解析器。 行为会随广告信令模式和广告元数据的不同组合而改变。
* 多个初始`PlacementInformations` `DefaultMediaPlayer`根据广告信令模式和要由`MediaPlayerClient`解析的广告元数据创建初始`PlacementInformations`的列表。

* 新的广告信令模式：自定义时间范围

   广告根据来自外部源（如JSON文件）的时间范围数据进行放置。