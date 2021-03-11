---
description: TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。
title: DRM事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# DRM事件{#drm-events}

TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。

要获得有关所有与DRM相关的事件的通知，请侦听`MediaPlayer`对象的DRM事件。`DRMMetadataInfoEvent`

| 事件 | 意义 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 新的DRM元数据可用。 |