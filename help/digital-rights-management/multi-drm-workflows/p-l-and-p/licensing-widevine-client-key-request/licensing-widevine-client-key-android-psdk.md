---
description: 客户端代码将数据传递到Android API。
title: Android PSDK上的关键请求工作流
exl-id: 3ff52c0d-0789-4fe5-bf9d-f03184bad488
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Android PSDK上的关键请求工作流{#key-request-workflow-on-android-psdk}

客户端代码将数据传递到Android API。

在Android上，您的客户端代码应使用以下API在许可证服务器URL中传递以及随附的许可证客户获取数据：

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

成功调用此API后，您的代码可以按常规方式开始播放内容。 如果您使用的是Expressplay，您可以将令牌作为许可证服务器URL的一部分或作为请求属性传递，然后从许可证服务器URL中剥离令牌。

某些Android设备同时支持Widevine和PlayReady。 在此类设备上，如果内容具有多个DRM标头，则客户可能希望强制PSDK使用特定DRM解密内容。 这可以在播放之前调用以下API来完成：

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```
