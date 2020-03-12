---
description: 通过MediaPlayerItem.timedMetadata属性，您可以访问从播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。
seo-description: 通过MediaPlayerItem.timedMetadata属性，您可以访问从播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。
seo-title: 清单标记通知
title: 清单标记通知
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 清单标记通知{#notifications-for-manifest-tags}

通过MediaPlayerItem.timedMetadata属性，您可以访问从播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。

您可以通过侦听以下事件来监视定时元数据，这些事件会向应用程序通知相关活动：

* `MediaPlayerItemEvent.ITEM_CREATED`:创建对象 `TimedMetadata` 后，可使用初始 `MediaPlayerItem` 列表。 此事件会在发生此情况时通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`:对于清单／播放列表定期刷新的实时／线性流，更新的播放列表／清单中可能会显示其他自定义标记，因此可能会向属性添加其他TimedMetadata对 `MediaPlayerItem.timedMetadata` 象。 此事件会在发生此情况时通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次创建新对 `TimedMetadata` 象时，都会由调度此事件 `MediaPlayer`。 对于在初始化阶段创建的对 `TimedMetadata` 象，不调度此事件。

