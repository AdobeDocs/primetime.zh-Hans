---
description: MediaPlayerItem.timedMetadata属性提供对所有TimedMetadata对象的访问，这些对象是从播放列表／清单标记或媒体流中的ID3标记创建的。
seo-description: MediaPlayerItem.timedMetadata属性提供对所有TimedMetadata对象的访问，这些对象是从播放列表／清单标记或媒体流中的ID3标记创建的。
seo-title: 清单标记通知
title: 清单标记通知
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 清单标记通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata属性提供对所有TimedMetadata对象的访问，这些对象是从播放列表／清单标记或媒体流中的ID3标记创建的。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

`MediaPlayerItem.hasTimedMetadata`属性指示当前媒体中是否存在订阅的自定义标记。 您可以通过侦听`Events.TimedMetadataEvent`来监视定时元数据，MediaPlayer实例每次创建新的`TimedMetadata`对象时都会调度该元数据。
