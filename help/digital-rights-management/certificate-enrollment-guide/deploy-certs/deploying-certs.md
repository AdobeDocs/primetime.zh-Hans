---
title: 部署证书
description: 部署证书
copied-description: true
exl-id: 649c4f24-f74e-4529-84a2-65bcd6d7677c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 部署证书{#deploy-certificates}

为了避免在许可证服务器上以明文形式提供PFX密码，Reference Implementation和Adobe Primetime DRM Server for Protected Streaming要求在配置文件中指定密码时对其进行加密。 参见 *使用Primetime DRM参考实施* 或 *使用Primetime DRM服务器* ，以获取有关运行扰频实用程序的说明。 其中每个都包含其自己的加扰实用程序，并且加密的密码不能在这两个许可证服务器实现之间互换。

要将证书和加扰密码部署到许可证服务器，请参见 *使用Primetime DRM参考实施* 或 *使用Primetime DRM服务器进行受保护的流*.
