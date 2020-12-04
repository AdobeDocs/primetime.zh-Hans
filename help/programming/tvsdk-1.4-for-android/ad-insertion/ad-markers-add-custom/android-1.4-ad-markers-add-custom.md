---
description: 通过使用自定义广告标记，您可以将主要内容的特定部分标记为与广告相关的内容句点。
seo-description: 通过使用自定义广告标记，您可以将主要内容的特定部分标记为与广告相关的内容句点。
seo-title: 添加自定义广告标记
title: 添加自定义广告标记
uuid: 5d8c8aaa-a4e7-499d-b70e-5c72007ec269
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 概述{#add-custom-ad-markers-overview}

通过使用自定义广告标记，您可以将主要内容的特定部分标记为与广告相关的内容句点。

当从实时事件记录内容，并且记录结果是一个HLS流时，此功能最有用。 录像包含一个HLS视频点播(VOD)流中的主要内容和广告相关内容。 录制过程不跟踪广告相关细分，因此与广告在主内容中的位置相关的信息会丢失。

您可能能够从其他带外源（如外部CMS系统）获取与广告内容周期定位相关的信息。 您可以定义自定义标记，通过自定义标记可将带外信息传递给时间轴管理器子系统。 其目的是标记与指定的广告相关内容匹配的内容部分，以使所有广告特定播放事件的触发方式与将这些自定义广告时段显式放置在播放器的时间线上的方式相同。

广告跟踪不是由TVSDK在内部处理的，例如何时广告由Adobe Primetime广告决策（以前称为Auditude）解析。 但是，TVSDK提供以下抽象，用于定义在时间轴上显示与广告相关的内容的方式：

* 广告中断

   广告中断是单个连续广告的有序列表。
* 个人广告

在每个广告的起始点和结束点分别为广告中断和广告触发播放事件。

TVSDK将广告跟踪事件派发到您的应用程序，以便您能够实施您自己的跟踪逻辑。 如果设置自定义广告标记，您将收到`onAdBreakStart`、`onAdStart`、`onAdProgress`、`onAdComplete`和`onAdBreakComplete`事件。
