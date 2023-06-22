---
description: 您可以使用PrimetimeDigital Rights Management(DRM)系统的功能来提供对视频内容的安全访问。 或者，您可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。
title: Widevine DRM
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Widevine DRM {#widevine-drm}

您可以使用PrimetimeDigital Rights Management(DRM)系统的功能来提供对视频内容的安全访问。 或者，您可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。

有关第三方DRM解决方案可用性的最新信息，请与您的Adobe代表联系。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以将Android本机Widevine DRM与HLS CMAF流结合使用。

>[!NOTE]
>
> Widevine CENC CTR方案要求最低Android版本4.4（API级别19）。
>
> Widevine CBCS方案要求最低Android版本7.1（API级别25）。

## 设置许可证服务器详细信息 {#license-server-details}

调用以下项 `com.adobe.mediacore.drm.DRMManager` 加载MediaPlayer资源之前的API：

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 参数 {#arguments-license-server}

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

## 提供自定义回调 {#custom-callback}

调用以下项 `com.adobe.mediacore.drm.DRMManager` 加载MediaPlayer资源之前的API。

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 参数 {#arguments-custom-callback}

* `callback`  — 要使用的MediaDrmCallback的自定义实施，而不是默认实施 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

有关详细信息，请参阅 [Android TVSDK 3.11 API文档](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## 获取当前加载的MediaPlayer资源的PSSH框 {#pssh-box-mediaplayer-resoource}

调用以下项 `com.adobe.mediacore.drm.DRMManager` API，最好在自定义回调实施中。

```java
public static byte[] getPSSH()
```

API返回与加载的Widevine媒体资源关联的Protection System特定的标头框。

有效框持续时间较短（在DRM实例创建和加载密钥之间）。 `MediaDrmCallback callback executeKeyRequest()` 可以使用它来自定义获取许可证密钥。

>[!NOTE]
>
> `getPSSH()` 仅单个播放器实例支持API。 多个播放器或“即时开启”功能应串行初始化，以接收正确的框。
