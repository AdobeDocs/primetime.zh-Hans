---
description: MediaPlayerItem.timedMetadata属性允许访问通过播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。
seo-description: MediaPlayerItem.timedMetadata属性允许访问通过播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。
seo-title: 清单标记通知
title: 清单标记通知
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 清单标记通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata属性允许访问通过播放列表／清单标记或媒体流中的ID3标记创建的所有TimedMetadata对象。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

该属 `MediaPlayerItem.hasTimedMetadata` 性指示当前媒体中是否存在订阅的自定义标记。 您可以通过监听定时元数据来监 `Events.TimedMetadataEvent`视该元数据，每次创建新对象时，MediaPlayer实例都会 `TimedMetadata` 调度该元数据。
