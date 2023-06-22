---
title: 部署证书概述
description: 部署证书概述
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 概述 {#deploy-certificates-overview}

要将证书添加到Adobe Primetime DRM属性文件，请使用私钥将PKCS#7文件转换为PFX文件，并生成PEM文件或DER文件。

* 当需要凭据（证书和私钥）时，Primetime DRM命令行工具和AdobeHTTP Dynamic Streaming打包程序需要PFX文件。 SDK、参考实施和Primetime DRM Server for Protected Streaming可以接受PFX文件，也可以使用存储在HSM上的凭据。
* 如果只需要证书，则大多数Primetime DRM组件都可以使用PEM文件、DER文件或HSM上的证书。 AdobeHTTP Dynamic Streaming打包程序仅接受证书的DER文件。
