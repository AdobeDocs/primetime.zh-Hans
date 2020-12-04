---
description: Adobe为不想开发和维护自己的Primetime DRM许可证服务器的Adobe PrimetimeDRM客户提供云DRM服务。 通过利用此服务，客户可以降低DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备颁发DRM许可证。 此DRM服务由Adobe托管和维护，可全天候正常运行。
seo-description: Adobe为不想开发和维护自己的Primetime DRM许可证服务器的Adobe PrimetimeDRM客户提供云DRM服务。 通过利用此服务，客户可以降低DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备颁发DRM许可证。 此DRM服务由Adobe托管和维护，可全天候正常运行。
seo-title: 背景
title: 背景
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# 背景{#background}

Adobe为不想开发和维护自己的Primetime DRM许可证服务器的Adobe PrimetimeDRM客户提供云DRM服务。 通过利用此服务，客户可以降低DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备颁发DRM许可证。 此DRM服务由Adobe托管和维护，可全天候正常运行。

>[!NOTE]
>
>Adobe PrimetimeDRM以前称为Adobe访问，在此之前，称为Flash Access。

## Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}包含什么

* 自定义身份验证／授权模块以及有关如何对您的内容进行自定义身份验证的说明。 有关详细文档，请参阅[!DNL Custom Authentication Entitlement]目录。
* 特定于云DRM的许可证服务器证书([!DNL .pem/.cer/.der])

* 特定于云DRM的许可证服务器传输证书([!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* 打包的DRM策略示例

   * **policy_24hr** -许可证在磁盘上缓存24小时。24小时后，必须获得新许可才能视图内容。 此工具包中的所有其他策略也具有24小时许可证缓存。
   * **policy_ios_remotekeyserver**  —— 在iOS设备上，将从Cloud DRM获取DRM许可证。此外，客户端将从云DRM获取所有AES解密密钥。 在越狱的iOS设备上不允许播放。

   * **policy_ios_localkeyserver**  —— 在iOS设备上，将从Cloud DRM获取DRM许可证。此外，客户端将从本地HTTP服务器而不是云DRM获取所有HLS AES解密密钥。 在越狱的iOS设备上不允许播放。

   * **policy_adobePass**  —— 客户端必须先进行身份验证(以前称为Adobe Pass)，否则许可证将被拒绝。

* Adobe策略管理器工具，用于创建其他DRM策略
* 用于打包的视频内容范例

