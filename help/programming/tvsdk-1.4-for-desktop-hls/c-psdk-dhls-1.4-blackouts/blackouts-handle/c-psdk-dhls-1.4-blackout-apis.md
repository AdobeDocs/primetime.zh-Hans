---
description: TVSDK提供在实施封锁期时有用的API元素，包括方法、元数据和通知。
seo-description: TVSDK提供在实施封锁期时有用的API元素，包括方法、元数据和通知。
seo-title: 封锁API元素
title: 封锁API元素
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 封锁API元素{#blackout-api-elements}

TVSDK提供在实施封锁期时有用的API元素，包括方法、元数据和通知。

在播放器中实施封锁期解决方案时，可以使用以下方法。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为后台资源。 如果 `replaceCurrentResource` 在此方法之后调用，则TVSDK将继续下载背景项的清单，直到您调用 `unregisterCurrentBackgroundItem`。

   * `unregisterCurrentBackgroundItem`  清除当前设置的背景资源并停止获取和解析背景清单。

* **BlackoutMetadata** 特定于封锁期的元数据类型。

   这允许您在TVSDK上设置不可搜索的范围( `TimeRange` 称为其 `nonseekableRange`他属性)。 TVSDK在用户每次搜索时检查这些范围(所需的搜索位 `nonseekableRange`置是否在a内)。 如果设置了查看器并且用户搜索到不可搜索的范围，则TVSDK会强制查看器到达该查看器的结束时间 `seekableRange`。

* **在此处开始****下一步默认元数据键通过设置为true或false在实时流上**`ENABLE_LIVE_PREROLL` 启用或禁用预卷。 如果为false，则TVSDK在内容播放之前不会对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中间辊没有影响。 默认值为true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子类型——当TVSDK检测到后台清单中的订阅标记时调度。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可搜索的范围中尝试搜索时调度。


