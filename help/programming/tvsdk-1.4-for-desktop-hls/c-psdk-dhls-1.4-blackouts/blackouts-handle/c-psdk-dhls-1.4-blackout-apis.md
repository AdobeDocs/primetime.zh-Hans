---
description: TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。
title: 封锁API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 封锁API元素{#blackout-api-elements}

TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。

在播放器中实施封锁解决方案时，可以使用以下方法。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为后台资源。如果在此方法之后调用`replaceCurrentResource`，则TVSDK将继续下载后台项的清单，直到您调用`unregisterCurrentBackgroundItem`。

   * `unregisterCurrentBackgroundItem`  清除当前设置的背景资源并停止获取和分析背景清单。

* **BlackoutMetadata** 特定于封锁的元数据类型。

   这允许您在TVSDK上设置不可搜索的范围（另一个名为`nonseekableRange`的`TimeRange`属性）。 每次用户搜索时，TVSDK都会检查这些范围（所需的搜索位置是否在`nonseekableRange`内）。 如果设置了查看器并用户搜索到不可搜索的范围，TVSDK会强制查看器到`seekableRange`的结束时间。

* **开始此** **** 处NEXTDefaultMetadataKeys通过设置为true或false在实时流上启 `ENABLE_LIVE_PREROLL` 用或禁用预卷。如果为false，则TVSDK在内容播放之前不会对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中间人没有影响。 默认值为true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子类型 — 当TVSDK检测到后台清单中的订阅标记时调度。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可搜索范围内尝试搜索时调度。


