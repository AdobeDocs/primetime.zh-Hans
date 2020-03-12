---
description: TVSDK将调度广告服务事件以响应定时元数据操作。
seo-description: TVSDK将调度广告服务事件以响应定时元数据操作。
seo-title: 广告服务／定时元数据事件
title: 广告服务／定时元数据事件
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 广告服务／定时元数据事件{#ad-serving-timed-metadata-events}

TVSDK将调度广告服务事件以响应定时元数据操作。

要获得所有此类相关事件的通知，请向对象注册以 `MediaPlayer` 下事件的事件监听器。

| 活动 | 意义 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已处理ID3定时元数据。 |
| TimedMetadataEvent。[TIMED_METADATA_KBIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 已处理定时元数据，但未检测到任何机会。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 定时元数据可用，并且未检测到任何机会。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 已处理定时元数据，且在后台清单中未检测到任何机会。 |