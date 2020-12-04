---
description: 您可以将Android本机Widevine DRM与DASH流结合使用。
seo-description: 您可以将Android本机Widevine DRM与DASH流结合使用。
seo-title: Widevine DRM
title: Widevine DRM
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# Widevine DRM {#widevine-drm}

您可以将Android本机Widevine DRM与DASH流结合使用。

在开始播放之前，请调用以下`com.adobe.mediacore.drm.DRMManager` API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

参数：

* `drm` -  `"com.widevine.alpha"` for widevine.

* `licenseServerURL` -接收许可证请求的Widevine许可证服务器的URL。
* `requestProperties` -包含要包含在传出许可证请求中的额外标头。

例如，在使用为Expressplay DRM打包的内容时，在播放前使用以下代码：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

