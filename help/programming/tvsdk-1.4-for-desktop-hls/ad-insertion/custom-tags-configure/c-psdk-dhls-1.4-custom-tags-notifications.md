---
description: MediaPlayerItem.timedMetadata属性允许您访问通过播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。
seo-description: MediaPlayerItem.timedMetadata属性允许您访问通过播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。
seo-title: 清单标记通知
title: 清单标记通知
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# 清单标记通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata属性允许您访问通过播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。

您可以通过监听以下事件来监视定时元数据，这些活动会通知您的应用程序相关的：

* `MediaPlayerItemEvent.ITEM_CREATED`:对象的初始 `TimedMetadata` 列表在创建后 `MediaPlayerItem` 可用。此事件会在发生此情况时通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`:对于清单／播放列表定期刷新的实时／线性流，更新的播放列表／清单中可能显示其他自定义标记，因此可能会向属性添加其他TimedMetadata `MediaPlayerItem.timedMetadata` 对象。此事件会在发生此情况时通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次创建新 `TimedMetadata` 对象时，都会由调度此事件 `MediaPlayer`。对于在初始化阶段创建的`TimedMetadata`对象，不调度此事件。

