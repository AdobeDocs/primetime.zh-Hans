---
description: TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。
title: DRM事件
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。

要接收有关所有DRM相关事件的通知，请侦听 `DRMMetadataInfoEvent` 的DRM事件 `MediaPlayer` 对象。

| 事件 | 含义 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 新的DRM元数据可用。 |
