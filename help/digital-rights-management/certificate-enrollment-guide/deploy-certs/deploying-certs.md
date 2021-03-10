---
title: 部署证书
description: 部署证书
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 部署证书{#deploy-certificates}

为避免许可证服务器上以明文形式提供PFX密码，Reference Implementation和Adobe Primetime DRM Server for Protected Streaming要求在配置文件中指定时加密该密码。 有关运行扰频实用程序的说明，请参阅&#x200B;*使用Primetime DRM参考实现*&#x200B;或&#x200B;*使用Primetime DRM Server*&#x200B;获取受保护流。 每个密码都包含自己的扰码实用程序，并且加密密码不能在这两个许可服务器实现之间互换。

要将证书和加扰的密码部署到您的许可证服务器，请参阅&#x200B;*使用Primetime DRM参考实现*&#x200B;或&#x200B;*使用Primetime DRM服务器进行受保护流*。
