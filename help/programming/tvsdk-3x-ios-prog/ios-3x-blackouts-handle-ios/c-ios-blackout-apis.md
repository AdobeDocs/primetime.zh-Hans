---
description: TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。
title: 封锁API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 封锁API元素{#blackout-api-elements}

TVSDK提供在实施封锁期（包括方法、元数据和通知）时有用的API元素。

在播放器中实施封锁解决方案时，可以使用以下方法。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为后台资源。如果在此方法之后调用`replaceCurrentItemWithPlayerItem`，则TVSDK将继续下载后台项的清单，直到您调用`unregisterCurrentBackgroundItem`、`stop`或`reset`。

   * `unregisterCurrentBackgroundItem` 将背景项设置为nil，并停止获取和分析背景清单。

* **特定于封锁** 的 `PTMetadata` PTMetadata.PTBlackoutMetadataA类。

   这允许您在TVSDK上设置不可搜索的范围（`CMTimeRanges`的数组）。 TVSDK在用户每次搜索时检查这些范围。 如果设置了查看器并用户搜索到不可搜索的范围，TVSDK将强制查看器到达不可搜索范围的末尾。

* **开始此** **** 处NEXTPTAdMetadata通过设置为YES或NO，在实时流上启 `enableLivePreroll` 用或禁用前滚。如果为否，则TVSDK在内容播放前不会对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中间人没有影响。 默认值为YES。

* **NSNoftigies**

   * `PTTimedMetadataChangedInBackgroundNotification`  — 当TVSDK检测到后台清单中的订阅标记并准备新实例时 `PTTimedMetadata` 发布。通知的对象是当前正在播放的`PTMediaPlayerItem`实例。 您可以使用`PTTimedMetadataKey`键从通知的`userInfo`词典中获取`PTTimedMetadata`实例。

   * `PTBackgroundManifestErrorNotification`  — 当媒体播放器完全无法加载后台清单时发布，即所有流URL都返回错误或无效响应。通知的对象是当前正在播放的`PTMediaPlayerItem`实例。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。
   * `INVALID_SEEK_WARNING` 在不可搜索范围（在中设置）中尝试搜索 `nonSeekableRanges` 时分 `PTBlackoutMetadata`派。