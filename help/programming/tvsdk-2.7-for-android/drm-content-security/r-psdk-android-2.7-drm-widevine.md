---
description: 您可以将Android本机Widevine DRM与DASH流结合使用。
title: Widevine DRM
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Widevine DRM {#widevine-drm}

您可以将Android本机Widevine DRM与DASH流结合使用。

调用以下项 `com.adobe.mediacore.drm.DRMManager` 开始播放之前的API：

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

参数：

* `drm` - `"com.widevine.alpha"` 为维德温。

* `licenseServerURL`  — 接收许可证请求的Widevine许可证服务器的URL。
* `requestProperties`  — 包含要包含在传出许可证请求中的额外标头。

例如，在使用为Expressplay DRM打包的内容时，在播放之前使用以下代码：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
