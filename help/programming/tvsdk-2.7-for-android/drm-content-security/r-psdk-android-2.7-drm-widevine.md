---
description: 您可以将Android本机Widevine DRM与DASH流结合使用。
title: Widevine DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Widevine DRM {#widevine-drm}

您可以将Android本机Widevine DRM与DASH流结合使用。

调用以下项 `com.adobe.mediacore.drm.DRMManager` 开始播放前的API：

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

参数：

* `drm` - `"com.widevine.alpha"` 为维德维恩干杯。

* `licenseServerURL`  — 接收许可证请求的Widevine许可证服务器的URL。
* `requestProperties`  — 包含要包含在传出许可证请求中的额外标头。

例如，当使用为Expressplay DRM打包的内容时，在播放之前使用以下代码：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
