---
description: TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。
seo-description: TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。
seo-title: 封锁API元素
title: 封锁API元素
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# 封锁API元素{#blackout-api-elements}

TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。

在播放器中实施封锁解决方案时，可以使用以下方法。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为背景资源。如果在此方法后调用`replaceCurrentResource`，则TVSDK将继续下载后台项的清单，直到您调用`unregisterCurrentBackgroundItem`。

   * `unregisterCurrentBackgroundItem`  清除当前设置的背景资源并停止读取和解析背景清单。

* **BlackoutMetadata** 特定于封锁的元数据类型。

   这允许您在TVSDK上设置不可搜索的范围（另一个名为`nonseekableRange`的`TimeRange`属性）。 TVSDK每次用户搜索时检查这些范围（所需的搜索位置是否在`nonseekableRange`内）。 如果设置了查看器并且用户搜索到不可搜索的范围，TVSDK会强制查看器到`seekableRange`的结束时间。

* **开始此** **** 处NEXTDefaultMetadataKeys通过设置为true或false在实时流上启 `ENABLE_LIVE_PREROLL` 用或禁用预卷。如果为false，则TVSDK在内容播放之前不会明确调用前置广告的广告服务器，因此不会播放前置广告。 这对中间人没有影响。 默认值为true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子类型——当TVSDK检测到后台清单中的订阅标记时调度。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可搜索的范围中尝试搜索时调度。


