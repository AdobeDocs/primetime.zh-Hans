---
seo-title: 部署证书概述
title: 部署证书概述
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 概述{#deploy-certificates-overview}

要向Adobe PrimetimeDRM属性文件添加证书，请使用私钥将PKCS#7文件转换为PFX文件，并生成PEM文件或DER文件。

* 当需要凭据（证书和私钥）时，Primetime DRM命令行工具和AdobeHTTP Dynamic Streaming打包程序需要PFX文件。 SDK、Reference Implementation和Primetime DRM Server for Protected Streaming可以接受PFX文件，还可以使用存储在HSM上的凭据。
* 当只需要证书时，大多数Primetime DRM组件可以在HSM上使用PEM文件、DER文件或证书。 AdobeHTTP Dynamic Streaming包装程序只接受证书的DER文件。