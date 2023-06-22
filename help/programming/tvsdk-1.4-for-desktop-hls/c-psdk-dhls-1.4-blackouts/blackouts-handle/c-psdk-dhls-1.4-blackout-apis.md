---
description: TVSDK提供了在实施封锁时有用的API元素，包括方法、元数据和通知。
title: 封锁API元素
exl-id: 9dae236b-0bd8-4fce-9163-628d4ed94f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 封锁API元素{#blackout-api-elements}

TVSDK提供了在实施封锁时有用的API元素，包括方法、元数据和通知。

在播放器中实施封锁解决方案时，您可以使用以下内容。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源另存为后台资源。 如果 `replaceCurrentResource` 在此方法之后调用，TVSDK将继续下载后台项目的清单，直到您调用 `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  清除当前设置的后台资源，并停止提取和分析后台清单。

* **BlackoutMetadata** 特定于封锁的元数据类型。

   这允许您设置不可搜索的范围(附加 `TimeRange` 已调用属性 `nonseekableRange`)。 TVSDK会检查这些范围(无论所需的搜寻位置是否位于 `nonseekableRange`)。 如果设置了该选项且用户试图进入不可搜索范围，TVSDK会强制查看器到达 `seekableRange`.

* **从此处开始（下一步）** **DefaultMetadataKey** 通过设置对实时流启用或禁用preroll `ENABLE_LIVE_PREROLL` 为true或false。 如果为false，则TVSDK不会在内容播放之前对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中端市场没有影响。 默认值为true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子类型 — 当TVSDK检测到后台清单中的订阅标记时调度。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码： 204000
      * 类型：警告
      * 后台清单下载出错。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可搜索范围内尝试搜寻时调度。
