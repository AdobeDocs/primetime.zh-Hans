---
description: 您可以完成Digital Rights Management(DRM)特定的工作流。
seo-description: 您可以完成Digital Rights Management(DRM)特定的工作流。
seo-title: Digital Rights Management
title: Digital Rights Management
uuid: 011605c7-50c4-4ad5-9961-8cd92d0e6fd8
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Digital Rights Management{#digital-rights-management}

您可以完成Digital Rights Management(DRM)特定的工作流。

您可以聆听`AdobePSDK.DRMMetadataInfoEvent`事件来处理DRM工作流:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## 添加Digital Rights Management{#add-digital-rights-management}

1. 添加`DRMMetadataInfoAvailableEvent`以获取`DRMMetadata`。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 在步骤1的行上方实施`onDRMMetadataInfoAvailable`部分。

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

1. 通过复制以下示例，为Widevine和PlayReady创建保护数据：

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
   >请确保更新资源类型，因为现在为DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 测试配置。