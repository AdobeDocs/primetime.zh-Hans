---
description: MediaPlayerItem.timedMetadata属性允许访问从播放列表/清单标记或从媒体流中的ID3标记创建的所有TimedMetadata对象。
title: 清单标记的通知
exl-id: a8a3cada-d796-460a-bd8f-fc4a2703e7f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 清单标记的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata属性允许访问从播放列表/清单标记或从媒体流中的ID3标记创建的所有TimedMetadata对象。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

此 `MediaPlayerItem.hasTimedMetadata` 属性指示当前媒体中是否存在订阅的自定义标记。 您可以通过侦听 `Events.TimedMetadataEvent`，MediaPlayer实例每次发送新的播放器时都会进行发送 `TimedMetadata` 对象已创建。
