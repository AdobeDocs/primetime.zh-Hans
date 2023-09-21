---
description: TVSDK调度服务质量(QoS)事件，以通知应用程序存在可能会影响QoS统计信息计算的事件，例如缓冲或搜寻。
title: QoS事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK调度服务质量(QoS)事件，以通知应用程序存在可能会影响QoS统计信息计算的事件，例如缓冲或搜寻。

要接收有关所有QoS相关事件的通知，请在注册事件侦听器 `MediaPlayer` 对象：

| 事件 | 含义 |
|---|---|
| 缓冲事件。[缓冲结束](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 缓冲结束。 |
| 缓冲事件。[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 已开始缓冲。 |
| SeekEvent。[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 搜寻已完成。 |
| SeekEvent。[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 正在开始搜寻。 |
| SeekEvent。[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | 由于当前的广告策略，TVSDK更改了搜寻位置。 |
