---
description: TVSDK调度广告服务事件以响应定时元数据操作。
title: 广告服务/定时元数据事件
exl-id: 875afa2a-a5cc-4192-91e2-5ba7b61abd57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 广告服务/定时元数据事件{#ad-serving-timed-metadata-events}

TVSDK调度广告服务事件以响应定时元数据操作。

要接收有关所有相关事件的通知，请将事件侦听器注册到 `MediaPlayer` 对象。

| 事件 | 含义 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已处理ID3定时元数据。 |
| TimedMetadataEvent。[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 已处理定时元数据，但未检测到机会。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 定时元数据可用，并且未检测到机会。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 已处理定时元数据，并且在后台清单中未找到任何机会。 |
