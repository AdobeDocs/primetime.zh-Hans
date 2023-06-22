---
description: TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲或搜寻。
title: QoS事件
exl-id: 7de28d00-12e2-4f2a-bb1b-53661e3578a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲或搜寻。

要接收有关所有QoS相关事件的通知，请将事件侦听器注册到 `MediaPlayer` 对象，用于以下事件：

| 事件 | 含义 |
|---|---|
| 缓冲事件。[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 缓冲完成。 |
| 缓冲事件。[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 已开始缓冲。 |
| SeekEvent。[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 搜寻已完成。 |
| SeekEvent。[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 正在开始搜寻。 |
| SeekEvent。[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | 由于当前的广告策略，TVSDK更改了搜寻位置。 |
