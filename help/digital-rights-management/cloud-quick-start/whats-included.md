---
description: Adobe为不希望开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供云DRM服务。 通过利用此服务，客户可以降低围绕DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备发放DRM许可证。 此DRM服务由Adobe托管和维护，全天候正常运行。
seo-description: Adobe为不希望开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供云DRM服务。 通过利用此服务，客户可以降低围绕DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备发放DRM许可证。 此DRM服务由Adobe托管和维护，全天候正常运行。
seo-title: 背景
title: 背景
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 背景 {#background}

Adobe为不希望开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供云DRM服务。 通过利用此服务，客户可以降低围绕DRM许可证发行的操作和开发复杂性。 Primetime Cloud DRM可向所有能运行支持Primetime浏览器TVSDK的视频应用程序（如iOS、Android、桌面和Xbox360）的设备发放DRM许可证。 此DRM服务由Adobe托管和维护，全天候正常运行。

>[!NOTE]
>
>Adobe Primetime DRM以前称为Adobe Access，之前称为Flash Access。

## Primetime Cloud DRM包含什么 {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* 自定义身份验证／授权模块以及有关如何对您的内容进行自定义身份验证的说明。 有关更多文档，请参阅该目 [!DNL Custom Authentication Entitlement] 录。
* 特定于DRM的云许可证服务器证书( [!DNL .pem/.cer/.der])

* 特定于DRM的云许可证服务器传输证书( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* 打包的DRM策略示例

   * **policy_24hr** —— 许可证在磁盘上缓存24小时。 24小时后，必须获得新许可才能查看内容。 此工具包中的所有其他策略也具有24小时许可证缓存。
   * **policy_ios_remotekeyserver** —— 在iOS设备上，将从Cloud DRM获取DRM许可证。 此外，客户端将从云DRM获取所有AES解密密钥。 在越狱的iOS设备上不允许播放。

   * **policy_ios_localkeyserver** —— 在iOS设备上，将从Cloud DRM获取DRM许可证。 此外，客户端将从本地HTTP服务器（而非Cloud DRM）获取所有HLS AES解密密钥。 在越狱的iOS设备上不允许播放。

   * **policy_adobePass** —— 客户端必须首先使用（以前称为Adobe Pass）进行身份验证，否则许可证将被拒绝。

* 用于创建其他DRM策略的Adobe策略管理器工具
* 用于打包的示例视频内容

