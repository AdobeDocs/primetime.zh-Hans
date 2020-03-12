---
description: TVSDK将根据DRM相关操作（如当新的DRM元数据可用时）调度数字版权管理(DRM)事件。 您的播放器可以实施响应这些事件的操作。
seo-description: TVSDK将根据DRM相关操作（如当新的DRM元数据可用时）调度数字版权管理(DRM)事件。 您的播放器可以实施响应这些事件的操作。
seo-title: DRM事件
title: DRM事件
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# DRM事件{#drm-events}

TVSDK将根据DRM相关操作（如当新的DRM元数据可用时）调度数字版权管理(DRM)事件。 您的播放器可以实施响应这些事件的操作。

要获得所有与DRM相关的事件的通知，请侦听以下内容：

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

以下示例展示了典型的进度：

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```

