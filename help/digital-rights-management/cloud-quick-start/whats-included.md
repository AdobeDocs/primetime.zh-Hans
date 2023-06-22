---
description: Adobe为不希望开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供了云DRM服务。 通过使用此服务，客户可以降低DRM许可证颁发的操作和开发复杂性。 Primetime Cloud DRM可以向能够运行启用了Primetime浏览器TVSDK的视频应用程序的所有设备(例如iOS、Android、台式机和Xbox360)颁发DRM许可证。 此DRM服务由Adobe托管和维护，全天候运行。
title: 背景
exl-id: bb5ad080-5b1d-43a6-8d0e-9b5735c82d96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 背景 {#background}

Adobe为不希望开发和维护自己的Primetime DRM许可证服务器的Adobe Primetime DRM客户提供了云DRM服务。 通过使用此服务，客户可以降低DRM许可证颁发的操作和开发复杂性。 Primetime Cloud DRM可以向能够运行启用了Primetime浏览器TVSDK的视频应用程序的所有设备(例如iOS、Android、台式机和Xbox360)颁发DRM许可证。 此DRM服务由Adobe托管和维护，全天候运行。

>[!NOTE]
>
>Adobe Primetime DRM以前称为Adobe访问，之前称为Flash Access。

## Primetime Cloud DRM包含哪些功能 {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* 自定义身份验证/授权模块和有关如何对内容进行自定义身份验证的说明。 有关更多文档，请参阅 [!DNL Custom Authentication Entitlement] 目录。
* 云DRM特定的许可证服务器证书( [!DNL .pem/.cer/.der])

* 云DRM特定的许可证服务器传输证书( [!DNL .pem/.cer/.der])

* Primetime Java脱机打包程序
* 打包的DRM策略示例

   * **policy_24hr**  — 许可证在磁盘上的缓存24小时。 24小时后，必须获得新许可证才能查看内容。 此工具包中的所有其他策略还具有24小时许可证缓存。
   * **policy_ios_remotekeyserver**  — 在iOS设备上，将从Cloud DRM获取DRM许可证。 此外，客户端将从云DRM获取所有AES解密密钥。 被监禁的iOS设备不允许播放。

   * **policy_ios_localkeyserver**  — 在iOS设备上，将从Cloud DRM获取DRM许可证。 此外，客户端将从本地HTTP服务器而不是云DRM获取所有HLS AES解密密钥。 被监禁的iOS设备不允许播放。

   * **policy_adobePass**  — 客户端必须首先通过(以前称为Adobe Pass)进行身份验证，否则许可证将被拒绝。

* Adobe策略管理器工具创建其他DRM策略
* 用于打包的视频内容示例
