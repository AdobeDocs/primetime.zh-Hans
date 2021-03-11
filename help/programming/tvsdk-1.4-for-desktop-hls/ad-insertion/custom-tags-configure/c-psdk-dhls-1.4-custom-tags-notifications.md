---
description: 通过MediaPlayerItem.timedMetadata属性，您可以访问从播放列表/清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。
title: 清单标记的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 清单标记{#notifications-for-manifest-tags}的通知

通过MediaPlayerItem.timedMetadata属性，您可以访问从播放列表/清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。

您可以通过侦听以下事件来监视计时元数据，这些活动会向您的应用程序通知相关的元数据：

* `MediaPlayerItemEvent.ITEM_CREATED`:在创建对象 `TimedMetadata` 后，可以使用对象 `MediaPlayerItem` 的初始列表。此事件会在发生此情况时通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`:对于清单/播放列表定期刷新的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此可能会向属性中添加其他TimedMetadata `MediaPlayerItem.timedMetadata` 对象。此事件会在发生此情况时通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次创建新 `TimedMetadata` 对象时，都会由调度此事件 `MediaPlayer`。不为在初始化阶段创建的`TimedMetadata`对象调度此事件。

