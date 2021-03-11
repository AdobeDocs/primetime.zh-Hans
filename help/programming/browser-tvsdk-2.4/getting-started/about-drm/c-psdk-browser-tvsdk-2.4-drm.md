---
description: 您可以完成Digital Rights Management(DRM)特定的工作流。
title: Digital Rights Management
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Digital Rights Management{#digital-rights-management}

您可以完成Digital Rights Management(DRM)特定的工作流。

您可以侦听`AdobePSDK.DRMMetadataInfoEvent`事件以处理DRM工作流:

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

1. 执行步骤1中行上方的`onDRMMetadataInfoAvailable`部分。

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
   >请确保您更新了资源类型，因为现在这是DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 测试配置。