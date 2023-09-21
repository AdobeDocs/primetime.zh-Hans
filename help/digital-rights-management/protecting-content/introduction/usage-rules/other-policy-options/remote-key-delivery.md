---
title: 远程和本地iOS密钥投放
description: 远程和本地iOS密钥投放
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 远程和本地iOS密钥投放 {#remote-and-local-ios-key-delivery}

Adobe Primetime支持将密钥交付到iOS客户端的以下选项：

* **远程**  — 按HTTP实时流(HLS)规范中指定的方式执行；M3U8清单指定了一个HTTPS路径，该路径包含用于解密流中以下加密段的AES密钥。 当您指定 `Remote` 在Primetime DRM策略中，客户端设备必须连接到远程HTTPS服务器才能获取AES密钥。

* **本地**  — 当您指定 `Local` 在Primetime DRM中，本地HTTPS服务器不是连接到AES密钥的互联网/网络，而是嵌入到iOS应用程序中，由其管理所有AES密钥请求。 在P应用程序中自动设置和配置嵌入式HTTPS服务器。 应用程序开发人员无需干预。

通过用于打包内容的Primetime DRM策略启用远程密钥投放。 如果要更改此设置，必须重新打包内容。 如果启用了远程密钥投放，则必须部署一个可以管理来自iOS客户端的密钥请求的Primetime DRM密钥服务器。 但是，其他平台上的客户端的工作流没有变化。

>[!NOTE]
>
>密钥投放选择仅影响iOS客户端。 所有其他使用HLS内容的设备，例如Android和Primetime on Desktop(Flash Player)，始终使用 `Local` 密钥投放，即使 `Remote` 已指定。
