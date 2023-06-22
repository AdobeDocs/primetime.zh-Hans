---
title: 颁发许可证以将远程密钥交付到iOS客户端(需要Adobe Primetime)
description: 颁发许可证以将远程密钥交付到iOS客户端(需要Adobe Primetime)
copied-description: true
exl-id: 91eecc25-16a9-4f8c-9307-83e70bb77d68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# 颁发许可证以将远程密钥交付到iOS客户端(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

要为需要为iOS设备远程交付密钥的内容颁发许可证，必须在中指定密钥服务器的许可证服务器证书 `HandlerConfiguration.setKeyServerCertificate()`.
