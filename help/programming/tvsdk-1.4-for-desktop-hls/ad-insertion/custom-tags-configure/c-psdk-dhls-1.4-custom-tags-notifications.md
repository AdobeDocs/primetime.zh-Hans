---
description: MediaPlayerItem.timedMetadata属性允许您访问从播放列表/清单标记或从媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。
title: 清单标记的通知
exl-id: 1a91fa47-edd5-4496-9755-17c906a3cf54
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 清单标记的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata属性允许您访问从播放列表/清单标记或从媒体流中的ID3标记创建的所有TimedMetadata对象。 MediaPlayerItem.hasTimedMetadata属性指示当前媒体中是否存在订阅的自定义标记。

您可以通过侦听以下事件来监视定时元数据，这些事件会通知您的应用程序相关活动：

* `MediaPlayerItemEvent.ITEM_CREATED`：初始列表 `TimedMetadata` 对象在以下位置后可用： `MediaPlayerItem` 创建。 发生此情况时，此事件会通知您的应用程序。

* `MediaPlayerItemEvent.ITEM_UPDATED`：对于定期刷新清单/播放列表的实时/线性流，更新的播放列表/清单中可能会显示其他自定义标记，因此可能会将其他TimedMetadata对象添加到 `MediaPlayerItem.timedMetadata` 属性。 发生此情况时，此事件会通知您的应用程序。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`：每当有新的 `TimedMetadata` 创建对象后，此事件将由 `MediaPlayer`. 此事件不会分派给 `TimedMetadata` 在初始化阶段创建的对象。
