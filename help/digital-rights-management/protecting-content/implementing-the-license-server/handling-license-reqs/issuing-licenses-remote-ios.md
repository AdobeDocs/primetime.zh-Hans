---
title: 颁发许可证以将远程密钥交付到iOS客户端(需要Adobe Primetime)
description: 颁发许可证以将远程密钥交付到iOS客户端(需要Adobe Primetime)
copied-description: true
exl-id: f9f13ab3-3394-4729-a64c-f28c67601e26
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 颁发许可证以将远程密钥交付到iOS客户端(需要Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

如果要为iOS设备需要远程密钥交付的内容颁发许可证，您需要在中指定密钥服务器的许可证服务器证书 `HandlerConfiguration.setKeyServerCertificate()`.
