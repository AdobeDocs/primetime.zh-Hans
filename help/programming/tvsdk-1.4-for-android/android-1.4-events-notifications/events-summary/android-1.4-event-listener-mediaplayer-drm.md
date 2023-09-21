---
description: TVSDK调度数字权限管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。
title: DRM事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK调度数字权限管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。

要收到有关所有DRM相关事件的通知，请注册以下项的 `MediaPlayer.DRMEventListener` 包括以下回调。

| 事件 | 含义 |
|---|---|
| [onDRMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | 新DRM元数据可用。 |
