---
description: TVSDK将根据DRM相关操作（如当新的DRM元数据可用时）调度数字版权管理(DRM)事件。
seo-description: TVSDK将根据DRM相关操作（如当新的DRM元数据可用时）调度数字版权管理(DRM)事件。
seo-title: DRM事件
title: DRM事件
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# DRM事件{#drm-events}

TVSDK将根据DRM相关操作（如当新的DRM元数据可用时）调度数字版权管理(DRM)事件。

要获得所有与DRM相关的事件的通知，请注册包含以 `MediaPlayer.DRMEventListener` 下回调的实现。

| 活动 | 意义 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo))`(DRMMetadataInfo drmMetadataInfo)` | 新的DRM元数据可用。 |

