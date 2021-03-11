---
description: MediaPlayerItem.timedMetadata属性提供对所有TimedMetadata对象的访问，这些对象是从播放列表/清单标记或媒体流中的ID3标记创建的。
title: 清单标记的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 清单标记{#notifications-for-manifest-tags}的通知

MediaPlayerItem.timedMetadata属性提供对所有TimedMetadata对象的访问，这些对象是从播放列表/清单标记或媒体流中的ID3标记创建的。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

`MediaPlayerItem.hasTimedMetadata`属性指示当前媒体中是否存在订阅的自定义标记。 您可以通过侦听`Events.TimedMetadataEvent`来监视定时元数据，每次创建新`TimedMetadata`对象时，MediaPlayer实例都会调度该元数据。
