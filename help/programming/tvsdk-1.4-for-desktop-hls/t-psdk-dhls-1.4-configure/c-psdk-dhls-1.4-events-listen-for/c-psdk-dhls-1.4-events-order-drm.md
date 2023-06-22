---
description: TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。 您的播放器可以实施操作来响应这些事件。
title: DRM事件
exl-id: 712347f3-f103-4c08-ad19-af1dd59ac549
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。 您的播放器可以实施操作来响应这些事件。

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
