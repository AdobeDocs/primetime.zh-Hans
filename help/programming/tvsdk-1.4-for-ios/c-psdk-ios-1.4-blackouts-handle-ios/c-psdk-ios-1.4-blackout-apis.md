---
description: TVSDK提供了在实施封锁期时有用的API元素，包括方法、元数据和通知。
title: 封锁API元素
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 封锁API元素{#blackout-api-elements}

TVSDK提供了在实施封锁期时有用的API元素，包括方法、元数据和通知。

在播放器中实施封锁解决方案时，您可以使用以下设置。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源另存为后台资源。 如果 `replaceCurrentItemWithPlayerItem` 此方法之后调用，TVSDK将继续下载后台项目的清单，直到调用 `unregisterCurrentBackgroundItem` ， `stop`，或 `reset` .

   * `unregisterCurrentBackgroundItem` 将后台项设置为nil并停止提取和分析后台清单。

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` 特定于中断的类。

  这允许您设置不可搜索的范围(一组 `CMTimeRanges`)。 TVSDK会在每次用户搜寻时检查这些范围。 如果设置了该参数并且用户搜寻到不可搜寻的范围，TVSDK会强制查看器搜寻到不可搜寻范围的结尾。

* **从此处开始（下一步）** **PTAdMetadata** 通过设置对实时流启用或禁用前置式播放 `enableLivePreroll` 更改为是或否。 如果为“否”，则TVSDK不会在内容播放之前对前置广告进行显式广告服务器调用，因此不会播放前置广告。 这对中端市场没有影响。 缺省值为YES。

* **NSNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification`  — 当TVSDK检测到后台清单中的订阅标记和新的标记时发布 `PTTimedMetadata` 实例已从中准备。 通知的对象是 `PTMediaPlayerItem` 当前正在播放的实例。 您可以获取 `PTTimedMetadata` 来自通知的实例 `userInfo` 词典使用 `PTTimedMetadataKey` 键。

   * `PTBackgroundManifestErrorNotification`  — 在媒体播放器完全无法加载后台清单时发布，即，所有流URL返回错误或无效响应。 通知的对象是 `PTMediaPlayerItem` 当前正在播放的实例。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码： 204000
      * 类型：警告
      * 后台清单下载时出错。

   * `INVALID_SEEK_WARNING` 在不可搜索范围内尝试搜寻时调度(在 `nonSeekableRanges` 在中设置 `PTBlackoutMetadata`)。
