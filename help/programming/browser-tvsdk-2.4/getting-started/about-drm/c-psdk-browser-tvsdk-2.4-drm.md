---
description: 您可以完成特定于Digital Rights Management(DRM)的工作流。
title: Digital Rights Management
exl-id: 5a40252b-2917-4341-bc64-8642432ddda9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

您可以完成特定于Digital Rights Management(DRM)的工作流。

你可以听到 `AdobePSDK.DRMMetadataInfoEvent` 用于处理DRM工作流的事件：

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## 添加Digital Rights Management {#add-digital-rights-management}

1. 添加 `DRMMetadataInfoAvailableEvent` 以获取 `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 实施 `onDRMMetadataInfoAvailable` 部分（位于步骤1中的行上方）。

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

1. 复制以下示例，为Widevine和PlayReady创建保护数据：

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
   >确保更新资源类型，因为现在为DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 测试您的配置。
