---
description: 您可以处理实时视频流中的封锁并在封锁期间提供替代内容。
title: 封锁API元素
exl-id: 8e4f1dc3-f2f6-4db9-b9d0-3e79d21032e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 封锁API元素{#blackout-api-elements}

您可以处理实时视频流中的封锁并在封锁期间提供替代内容。

当实时流中发生中断时，您的播放器会使用事件处理程序来检测该中断，并向没有资格观看主流的用户提供替代内容。 您的播放器会检测封锁期的开始和结束，将播放从主流切换到备用流，并在封锁期结束时切换回主流。

要在实时流中处理封锁，请执行以下操作：

1. 通过订阅实时流清单中的封锁标记，将应用程序设置为检测封锁标记。

   TVSDK本身不会检测封锁标记；您必须订阅封锁标记，才能在解析清单文件期间遇到标记时接收通知。
1. 为播放器订阅的标记（在本例中为“播放”和“封锁”标记）创建事件侦听器。

   当播放器在前台（主内容）或后台（备用内容）流清单中订阅（例如，阻止标记）的标记发生时，TVSDK将调度 `TimedMetadataEvent` 并创建 `TimedMetadataObject` 对于 `TimedMetadataEvent`.

1. 为前台和后台流的定时元数据事件实施处理程序。

   在这些处理程序中，从定时元数据事件对象获取封锁期的开始和结束时间。
1. 创建用于在封锁期开始和结束时切换内容的方法。

   当中断期开始时，将主内容切换到后台，并将替代内容切换到主流。 继续获取并解析后台的原始清单，并继续检查“封锁结束”标记，以便播放器能够在封锁结束时重新加入原始流。
1. 如果播放流上的封锁期在DVR中，请更新不可搜索的范围。

   跟踪和处理 `TimedMetadata` 在后台流中，通过准备和更新封锁不可搜索的范围。

TVSDK提供了在实施封锁时有用的API元素，包括方法、元数据和通知。

在播放器中实施封锁解决方案时，您可以使用以下内容。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源另存为后台资源。 如果 `replaceCurrentResource` 在此方法之后调用，TVSDK将继续下载后台项目的清单，直到您调用 `unregisterCurrentBackgroundItem`， `release`，或 `reset`.

   * `unregisterCurrentBackgroundItem` 将后台项设置为null并停止提取和分析后台清单。

* **BlackoutMetadata** -

   特定于封锁的元数据类。

   这允许您设置不可搜索的范围(一个数组 `TimeRanges`)。 TVSDK会在每次用户搜寻时检查这些范围。 如果设置了该参数并且用户搜寻到不可搜寻的范围，TVSDK会强制查看器搜寻到不可搜寻范围的结尾。

* **从此处开始下一页广告元数据** 通过设置对实时流启用或禁用preroll `enableLivePreroll` 为true或false。 如果为false，则TVSDK不会在内容播放之前对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中端市场没有影响。 默认值为true。

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem`  — 在后台清单中检测到订阅标记和新的 `TimedMetadata` 实例已从中准备好。 此 `TimedMetadata` 实例将作为参数调度。

   * `onBackgroundManifestFailed`  — 在媒体播放器完全无法加载后台清单时调度，即，所有流URL返回错误或无效响应。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码： 204000
      * 类型：警告
      * 后台清单下载出错。
