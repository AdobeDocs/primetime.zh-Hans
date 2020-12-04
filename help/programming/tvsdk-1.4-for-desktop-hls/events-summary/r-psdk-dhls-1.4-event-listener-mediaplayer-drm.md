---
description: TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。
seo-description: TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。
seo-title: DRM事件
title: DRM事件
uuid: f1da5b31-3fad-4bb4-8aa3-3925d5f0e123
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# DRM事件{#drm-events}

TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。

要获得所有与DRM相关的事件的通知，请监听`MediaPlayer`对象的DRM事件的`DRMMetadataInfoEvent`。

| 事件 | 意义 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 有新的DRM元数据可用。 |