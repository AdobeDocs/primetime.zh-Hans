---
description: 您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。
seo-description: 您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。
seo-title: Widevine DRM
title: Widevine DRM
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Widevine DRM {#widevine-drm}

您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。

有关第三方DRM解决方案可用性的最新信息，请与Adobe代表联系。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以将Android本机Widevine DRM与DASH流结合使用。

在开始播放之 `com.adobe.mediacore.drm.DRMManager` 前调用以下API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

参数：

* `drm` - `"com.widevine.alpha"` for widevine.

* `licenseServerURL` -接收许可证请求的Widevine许可证服务器的URL。
* `requestProperties` -包含要包含在传出许可证请求中的额外标题。

例如，在使用为Expressplay DRM打包的内容时，请在播放前使用以下代码：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
