---
description: 您可以使用PrimetimeDigital Rights Management(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。
title: Widevine DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Widevine DRM {#widevine-drm}

您可以使用PrimetimeDigital Rights Management(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成解决方案的替代方案。

有关第三方DRM解决方案可用性的最新信息，请与Adobe代表联系。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以将Android本机Widevine DRM与HLS CMAF流一起使用。

>[!NOTE]
>
> Widevine CENC CTR方案要求最低版本为Android 4.4（API级别19）。
>
> Widevine CBCS Scheme要求最低版本为Android 7.1(API Level 25)。

## 设置许可证服务器详细信息{#license-server-details}

在加载MediaPlayer资源之前，请调用以下`com.adobe.mediacore.drm.DRMManager` API:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 参数{#arguments-license-server}

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

## 提供自定义回调{#custom-callback}

在加载MediaPlayer资源之前，请调用以下`com.adobe.mediacore.drm.DRMManager` API。

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 参数{#arguments-custom-callback}

* `callback` - MediaDrmCallback的自定义实现，以代替默认 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`。

有关详细信息，请参阅[Android TVSDK 3.11 API文档](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html)。

## 获取当前加载的MediaPlayer资源{#pssh-box-mediaplayer-resoource}的PSSH框

调用以下`com.adobe.mediacore.drm.DRMManager` API，最好在自定义回调实现中。

```java
public static byte[] getPSSH()
```

API返回与加载的Widevine媒体资源关联的保护系统特定标头框。

有效框在较短的时间内可用（在创建DRM实例和加载密钥之间）。 `MediaDrmCallback callback executeKeyRequest()` 可以使用它自定义获取许可证密钥。

>[!NOTE]
>
> `getPSSH()` 仅单播放器实例支持API。多个播放器或“即时启动”功能应依次初始化，以接收正确的框。
