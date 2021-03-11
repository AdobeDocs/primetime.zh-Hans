---
title: 部署证书概述
description: 部署证书概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 概述{#deploy-certificates-overview}

要向Adobe Primetime DRM属性文件添加证书，请使用私钥将PKCS#7文件转换为PFX文件，并生成PEM文件或DER文件。

* 当需要凭据（证书和私钥）时，Primetime DRM命令行工具和AdobeHTTP Dynamic Streaming打包程序需要PFX文件。 SDK、参考实施和用于受保护流的Primetime DRM服务器可以接受PFX文件，也可以使用存储在HSM上的凭据。
* 当仅需要证书时，大多数Primetime DRM组件可以在HSM上使用PEM文件、DER文件或证书。 AdobeHTTP Dynamic Streaming打包程序只接受DER文件作为证书。