---
description: 您可以完成特定于数字版权管理(DRM)的工作流程。
seo-description: 您可以完成特定于数字版权管理(DRM)的工作流程。
seo-title: 数字版权管理
title: 数字版权管理
uuid: 011605c7-50c4-4ad5-9961-8cd92d0e6fd8
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96

---


# 数字版权管理 {#digital-rights-management}

您可以完成特定于数字版权管理(DRM)的工作流程。

您可以侦听事件以 `AdobePSDK.DRMMetadataInfoEvent` 处理DRM工作流：

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## 添加数字版权管理 {#add-digital-rights-management}

1. 添加 `DRMMetadataInfoAvailableEvent` 以获取 `DRMMetadata`。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 在步骤 `onDRMMetadataInfoAvailable` 1中的行上方实施该部分。

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. 在setupVideo方法中创建DRMManager。

   ```js
   var drmManager = player.drmManager;
   ```

1. 通过复制以下示例为Widevine和PlayReady创建保护数据：

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. 将保护数据添加到drmManager。

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. 将资源URL更改为DASH测试流。

   >[!TIP]
   >
   >请确保更新资源类型，因为这现在是DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 测试配置。