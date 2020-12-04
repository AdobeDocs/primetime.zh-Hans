---
description: 浏览器TVSDK提供DRM界面，可用于播放由不同DRM解决方案（包括FairPlay、PlayReady和Widevine）保护的内容。
seo-description: 浏览器TVSDK提供DRM界面，可用于播放由不同DRM解决方案（包括FairPlay、PlayReady和Widevine）保护的内容。
seo-title: DRM界面概述
title: DRM界面概述
uuid: b553ebad-8310-4517-8d97-ef8a1c5f4340
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# DRM接口概述{#drm-interface-overview}

浏览器TVSDK提供DRM界面，可用于播放由不同DRM解决方案（包括FairPlay、PlayReady和Widevine）保护的内容。

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM支持使用Microsoft PlayReady（在Windows 8.1和Edge的Internet Explorer上）和Widevine（在Google Chrome上）DRM系统保护的MPEG-Dash流。 DRM支持Safari上受FairPlay保护的HLS流。

DRM工作流的关键接口是`DRMManager`。 可通过MediaPlayer实例获取对`DRMManager`实例的引用：

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

以下是播放受DRM保护的内容的高级工作流：

1. 要附加浏览器TVSDK将在受保护流的许可证获取过程中使用的DRM系统特定数据，请在调用`mediaPlayer.replaceCurrentResource`之前进行以下调用：

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. 如果同一内容应用于不同浏览器中的不同DRM系统，则可为多个DRM系统指定保护数据。

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. 如果未设置保护数据，则从DRM系统的PSSH框（如果适用）检索许可证URL等必要信息。

   >[!TIP]
   >
   >指定保护数据将覆盖在PSSH框中指定的许可证URL。

1. 默认情况下，DRM许可证的会话类型是临时的，这意味着在会话关闭后不存储许可证。

   可以使用`DRMManager`中的API指定会话类型。  为了向后兼容，会话类型包括`temporary`、`persistent-license`、`persistent-usage-record`和`persistent`。

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 当使用的`sessionType`为`persistent-license`或`persistent`时，可以通过调用`DRMManager.returnLicense`返回DRM许可证。

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```

