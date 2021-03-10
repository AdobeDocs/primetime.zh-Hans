---
description: 客户端代码将数据传递到Android API。
title: Android PSDK上的密钥请求工作流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Android PSDK{#key-request-workflow-on-android-psdk}上的密钥请求工作流

客户端代码将数据传递到Android API。

在Android上，您的客户端代码应使用以下API传入许可证服务器URL和随附的许可证获取数据：

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

成功调用此API后，您的代码便可以按常规方式开始内容播放。 如果您使用的是Expressplay，则可以将令牌作为许可证服务器URL的一部分或作为请求属性进行传递，并从许可证服务器URL中删除令牌。

某些Android设备同时支持Widevine和PlayReady。 在此类设备上，如果内容具有多个DRM头，则客户可能希望强制PSDK使用特定DRM解密内容。 这可以通过在播放前调用以下API来实现：

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

