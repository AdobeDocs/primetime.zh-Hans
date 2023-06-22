---
description: 浏览器TVSDK提供了一个DRM界面，您可以使用它来播放受不同DRM解决方案（包括FairPlay、PlayReady和Widevine）保护的内容。
title: DRM界面概述
exl-id: aa13f042-4472-4fc3-b7ba-61746b8e024a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# DRM界面概述{#drm-interface-overview}

浏览器TVSDK提供了一个DRM界面，您可以使用它来播放受不同DRM解决方案（包括FairPlay、PlayReady和Widevine）保护的内容。

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM支持适用于受Microsoft PlayReady（在Windows 8.1和Edge上的Internet Explorer上）和Widevine(在Google Chrome上) DRM系统保护的MPEG-Dash流。 DRM支持适用于受FairPlay保护的Safari上的HLS流。

DRM工作流的关键界面是 `DRMManager`. 对的引用 `DRMManager` 可通过MediaPlayer实例获取实例：

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

以下是受DRM保护内容的播放的高级工作流：

1. 要附加浏览器TVSDK将在受保护流的许可证获取过程中使用的DRM系统特定数据，请在调用之前进行以下调用 `mediaPlayer.replaceCurrentResource`：

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

1. 如果相同的内容预期在不同浏览器中可以与不同的DRM系统一起使用，则可以为多个DRM系统指定保护数据。

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

1. 如果未设置保护数据，则会从DRM系统的PSSH框中检索必要信息（如许可证URL）（如果适用）。

   >[!TIP]
   >
   >指定保护数据将覆盖PSSH框中指定的许可证URL。

1. 默认情况下，DRM许可证的会话类型是临时的，这意味着在会话关闭后不会存储许可证。

   您可以在以下位置使用API指定会话类型： `DRMManager`.  为了向后兼容，会话类型包括 `temporary`， `persistent-license`， `persistent-usage-record`、和 `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 当 `sessionType` 已使用 `persistent-license` 或 `persistent`，可以通过调用 `DRMManager.returnLicense`.

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
