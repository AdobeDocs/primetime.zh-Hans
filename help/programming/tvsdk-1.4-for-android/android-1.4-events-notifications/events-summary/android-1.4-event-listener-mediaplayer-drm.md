---
description: TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。
title: DRM事件
exl-id: 8a3bd8c7-1e76-4d26-8f88-e29eb0a0e1b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。

要接收有关所有DRM相关事件的通知，请注册以下实施 `MediaPlayer.DRMEventListener` 包括以下回调。

| 事件 | 含义 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | 新的DRM元数据可用。 |
