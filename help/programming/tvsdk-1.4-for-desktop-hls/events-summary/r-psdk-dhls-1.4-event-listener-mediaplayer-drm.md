---
description: TVSDK调度数字权限管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。
title: DRM事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK调度数字权限管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。

要接收有关所有DRM相关事件的通知，请侦听 `DRMMetadataInfoEvent` 的DRM事件 `MediaPlayer` 对象。

| 事件 | 含义 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 新DRM元数据可用。 |
