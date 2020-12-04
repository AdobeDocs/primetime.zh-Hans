---
description: TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。
seo-description: TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。
seo-title: 封锁API元素
title: 封锁API元素
uuid: ddc81558-4218-44d2-92df-15926c7c96b3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 封锁API元素{#blackout-api-elements}

TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。

在播放器中实施封锁解决方案时，可以使用以下方法。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为背景资源。如果在此方法后调用`replaceCurrentItemWithPlayerItem`，则TVSDK将继续下载后台项的清单，直到您调用`unregisterCurrentBackgroundItem`、`stop`或`reset`。

   * `unregisterCurrentBackgroundItem` 将背景项设置为零，并停止获取和分析背景清单。

* **PTMetadata.** PTBlackoutMetadata `PTMetadata` 特定于封锁的类。

   这允许您在TVSDK上设置不可搜索的范围（`CMTimeRanges`的数组）。 TVSDK在用户每次搜索时检查这些范围。 如果设置了查看器并且用户搜索到不可搜索的范围，TVSDK会强制查看器到达不可搜索范围的末尾。

* **开始此** **** 处NEXTPTAdMetadata通过设置为“是”或“否”，在实时流上 `enableLivePreroll` 启用或禁用预滚动。如果为否，则TVSDK在内容播放前不会明确调用前置广告的广告服务器，因此不会播放前置广告。 这对中间人没有影响。 默认值为YES。

* **NSNoftigies**

   * `PTTimedMetadataChangedInBackgroundNotification` -当TVSDK检测到后台清单中的订阅标记并准备了新 `PTTimedMetadata` 实例时发布。通知的对象是当前正在播放的`PTMediaPlayerItem`实例。 您可以使用`PTTimedMetadataKey`键从通知的`userInfo`字典中获取`PTTimedMetadata`实例。

   * `PTBackgroundManifestErrorNotification` -当媒体播放器完全无法加载后台清单时发布，即所有流URL都返回错误或无效响应。通知的对象是当前正在播放的`PTMediaPlayerItem`实例。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。
   * `INVALID_SEEK_WARNING` 在不可搜索范围（在中设置）中尝试搜 `nonSeekableRanges` 索时 `PTBlackoutMetadata`调度。


