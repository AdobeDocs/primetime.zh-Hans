---
description: MediaPlayerItem.timedMetadata属性提供对从播放列表/清单标记或从媒体流中的ID3标记创建的所有TimedMetadata对象的访问权限。
title: 清单标记的通知
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 清单标记的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata属性提供对从播放列表/清单标记或从媒体流中的ID3标记创建的所有TimedMetadata对象的访问权限。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

此 `MediaPlayerItem.hasTimedMetadata` 属性指明当前媒体中是否存在订阅的自定义标记。 您可以通过侦听 `Events.TimedMetadataEvent`，每次创建新播放器时，MediaPlayer实例都会调度该队列 `TimedMetadata` 对象已创建。
