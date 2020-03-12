---
description: TVSDK提供在实施封锁期时有用的API元素，包括方法、元数据和通知。
seo-description: TVSDK提供在实施封锁期时有用的API元素，包括方法、元数据和通知。
seo-title: 封锁API元素
title: 封锁API元素
uuid: f87f4ed0-3f97-48bd-bceb-28357a978964
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 封锁API元素 {#blackout-api-elements}

TVSDK提供在实施封锁期时有用的API元素，包括方法、元数据和通知。

在播放器中实施封锁期解决方案时，可以使用以下方法。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 将当前加载的资源保存为后台资源。 如果 `replaceCurrentItemWithPlayerItem` 在此方法之后调用，则TVSDK将继续下载背景项的清单，直到您调用 `unregisterCurrentBackgroundItem` 、 `stop`或为止 `reset` 。

   * `unregisterCurrentBackgroundItem` 将背景项设置为nil，并停止获取和解析背景清单。

* **PTMetadata.PTBlackoutMetadata**`PTMetadata` 特定于封锁期的类。

   这允许您在TVSDK上设置不可搜索的范围( `CMTimeRanges`一组)。 TVSDK在用户每次搜索时检查这些范围。 如果设置了查看器并且用户搜索到不可搜索的范围，则TVSDK会强制查看器到达不可搜索范围的末尾。

* **从此处开始****下一个PTAd元数据通过设置为“是”或“否** ”，在实时流上启用或禁用预 `enableLivePreroll` 滚动功能。 如果为否，则TVSDK在内容播放之前不会对前置广告进行明确的广告服务器调用，因此不会播放前置广告。 这对中间辊没有影响。 默认值为YES。

* **NSNoftigies**

   * `PTTimedMetadataChangedInBackgroundNotification` -当TVSDK检测到后台清单中的订阅标记并准备了新实 `PTTimedMetadata` 例时发布。 通知的对象是当前 `PTMediaPlayerItem` 正在播放的实例。 您可以使用 `PTTimedMetadata` 键从通知的词典 `userInfo` 中提取实 `PTTimedMetadataKey` 例。

   * `PTBackgroundManifestErrorNotification` -当媒体播放器完全无法加载后台清单时发布，即所有流URL返回错误或无效响应。 通知的对象是当前 `PTMediaPlayerItem` 正在播放的实例。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代码：204000
      * 类型：警告
      * 后台清单下载时出错。
   * `INVALID_SEEK_WARNING` 在不可搜索范围（在中设置）中尝试搜索 `nonSeekableRanges` 时分 `PTBlackoutMetadata`派。