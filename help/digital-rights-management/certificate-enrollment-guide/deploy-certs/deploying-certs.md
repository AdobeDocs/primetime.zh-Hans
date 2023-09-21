---
title: 部署证书
description: 部署证书
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 部署证书{#deploy-certificates}

为避免在许可证服务器上以明文形式提供PFX密码，Reference Implementation和Adobe Primetime DRM Server for Protected Streaming在配置文件中指定时要求加密密码。 请参阅 *使用Primetime DRM参考实施* 或 *使用Primetime DRM服务器* ，以获取有关运行扰频实用程序的说明。 其中每个模块都包含其自己的加密实用程序，并且加密的密码在两个License Server实现之间不可互换。

要将证书和加密密码部署到许可证服务器，请参见 *使用Primetime DRM参考实施* 或 *使用用于受保护流的Primetime DRM服务器*.
