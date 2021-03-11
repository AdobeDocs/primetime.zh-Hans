---
description: 您可以将Android本机Widevine DRM与DASH流一起使用。
title: Widevine DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Widevine DRM {#widevine-drm}

您可以将Android本机Widevine DRM与DASH流一起使用。

开始播放前，请调用以下`com.adobe.mediacore.drm.DRMManager` API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

参数：

* `drm` - `"com.widevine.alpha"` 维德文。

* `licenseServerURL`  — 接收许可证请求的Widevine许可证服务器的URL。
* `requestProperties`  — 包含要包含在传出许可证请求中的额外标头。

例如，在使用为Expressplay DRM打包的内容时，请在播放前使用以下代码：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

