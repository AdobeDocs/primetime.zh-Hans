---
title: 远程和本地iOS密钥投放
description: 远程和本地iOS密钥投放
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# 远程和本地iOS密钥投放{#remote-and-local-ios-key-delivery}

Adobe Primetime支持以下选项，用于iOS客户端的关键投放:

* **远程**  — 按照HTTP实时流(HLS)规范中的指定执行；M3U8清单指定包含AES密钥的HTTPS路径，该密钥应用于解密流中的以下加密段。在Primetime DRM策略中指定`Remote`时，客户端设备必须连接到远程HTTPS服务器才能获取AES密钥。

* **本地**  — 当您在Primetime DRM中 `Local` 指定而不是连接到AES密钥的因特网/网络时，本地HTTPS服务器会嵌入到iOS应用程序中，然后iOS应用程序会管理所有AES密钥请求。嵌入的HTTPS服务器会在P应用程序中自动设置和配置。 应用程序开发人员无需干预。

远程密钥投放通过用于打包内容的Primetime DRM策略启用。 如果要更改此设置，必须重新打包内容。 如果启用远程密钥投放，则必须部署能够管理来自iOS客户端的密钥请求的Primetime DRM密钥服务器。 但是，对于其他平台上的客户端，工作流没有更改。

>[!NOTE]
>
>键投放选择仅影响iOS客户端。 使用HLS内容的所有其他设备(如Android和Primetime on Desktop(Flash Player))始终使用`Local`键投放，即使已指定`Remote`。

