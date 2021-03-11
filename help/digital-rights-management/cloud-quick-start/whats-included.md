---
description: Adobe为不想开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供云DRM服务。 通过利用此服务，客户可以降低DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备颁发DRM许可证。 此DRM服务由Adobe托管和维护，可全天候正常运行。
title: 背景
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 背景{#background}

Adobe为不想开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供云DRM服务。 通过利用此服务，客户可以降低DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备颁发DRM许可证。 此DRM服务由Adobe托管和维护，可全天候正常运行。

>[!NOTE]
>
>Adobe Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

## Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}包含什么

* 自定义身份验证/授权模块以及有关如何对您的内容使用自定义身份验证的说明。 有关详细文档，请参阅[!DNL Custom Authentication Entitlement]目录。
* 云DRM特定的许可证服务器证书([!DNL .pem/.cer/.der])

* 特定于云DRM的许可证服务器传输证书([!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* 打包的DRM策略示例

   * **policy_24hr-**  Licenses cache on disk 24 hors.24小时后，必须获得新许可才能视图内容。 此工具包中的所有其他策略也具有24小时许可证缓存。
   * **policy_ios_remotekeyserver**  — 在iOS设备上，将从Cloud DRM获取DRM许可证。此外，客户端将从云DRM获取所有AES解密密钥。 在越狱的iOS设备上不允许播放。

   * **policy_ios_localkeyserver**  — 在iOS设备上，将从Cloud DRM获取DRM许可证。此外，客户端将从本地HTTP服务器（而非云DRM）获取所有HLS AES解密密钥。 在越狱的iOS设备上不允许播放。

   * **policy_adobePass**  — 客户端必须先进行身份验证(以前称为Adobe Pass)，否则许可证将被拒绝。

* Adobe策略管理器工具，用于创建其他DRM策略
* 用于打包的视频内容示例

