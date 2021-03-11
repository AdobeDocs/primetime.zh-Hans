---
description: 您可以处理实时视频流中的封锁期，并在封锁期期间提供替代内容。
title: 封锁API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# 封锁API元素{#blackout-api-elements}

您可以处理实时视频流中的封锁期，并在封锁期期间提供替代内容。

当实时流中发生封锁时，您的播放器使用事件处理函数检测封锁并向那些不合格观看主流的用户提供替代内容。 您的播放器检测封锁期的开始和结束，将主流的播放切换到备用流，并在封锁期结束时切换回主流。

要处理实时流中的封锁：

1. 通过订阅实时流清单中的封锁标签，设置应用程序以检测封锁标签。

   TVSDK本身不检测封锁标签；您必须订阅封锁标签才能在清单文件解析期间遇到标签时接收通知。
1. 为播放器订阅的标签创建事件监听器（在此例中为PLAYBACK和LACOUSE标签）。

   当播放器在前景（主内容）或背景（备用内容）流清单中订阅（例如封锁标记）的标记时，TVSDK将调度`TimedMetadataEvent`并为`TimedMetadataEvent`创建`TimedMetadataObject`。

1. 为前台和后台流的定时元数据事件实现处理函数。

   在这些处理函数中，从定时元数据事件对象获取封锁期的开始和结束时间。
1. 创建用于在封锁期的开始和结束时切换内容的方法。

   当封锁期开始时，将主内容切换到后台，并将备用内容切换为主流。 继续在后台提取和分析原始清单，并继续检查“封锁结束”标签，以便在封锁结束时播放器可以重新加入原始流。
1. 如果封锁范围在播放流的DVR中，则更新不可查看的范围。

   通过准备和更新封锁不可搜索范围，跟踪并处理后台流上的`TimedMetadata`。

TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。

在播放器中实施封锁解决方案时，可以使用以下方法。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为后台资源。如果在此方法之后调用`replaceCurrentResource`，则TVSDK将继续下载后台项的清单，直到您调用`unregisterCurrentBackgroundItem`、`release`或`reset`。

   * `unregisterCurrentBackgroundItem` 将背景项设置为null并停止获取和分析背景清单。

* **BlackoutMetadata** -

   特定于封锁的元数据类。

   这允许您在TVSDK上设置不可搜索的范围（`TimeRanges`的数组）。 TVSDK在用户每次搜索时检查这些范围。 如果设置了查看器并用户搜索到不可搜索的范围，TVSDK将强制查看器到达不可搜索范围的末尾。

* **开始此处下** 一个广告元数据通过设置为true或false在实时流上启 `enableLivePreroll` 用或禁用预卷。如果为false，则TVSDK在内容播放之前不会对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中间人没有影响。 默认值为true。

* **MediaPlayer.LacolitesEventListener**

   * `onTimedMetadataInBackgroundItem`  — 当检测到后台清单中的订阅标记并准备了新实 `TimedMetadata` 例时调度。`TimedMetadata`实例作为参数调度。

   * `onBackgroundManifestFailed`  — 当媒体播放器完全无法加载后台清单时调度，即所有流URL都返回错误或无效响应。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。