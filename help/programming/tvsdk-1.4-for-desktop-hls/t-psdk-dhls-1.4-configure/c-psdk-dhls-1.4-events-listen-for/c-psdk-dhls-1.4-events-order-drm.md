---
description: TVSDK调度数字权限管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。 您的播放器可以实施操作来响应这些事件。
title: DRM事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK调度数字权限管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。 您的播放器可以实施操作来响应这些事件。

要接收有关所有DRM相关事件的通知，请监听以下内容：

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

以下示例显示了一个典型的行进：

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```
