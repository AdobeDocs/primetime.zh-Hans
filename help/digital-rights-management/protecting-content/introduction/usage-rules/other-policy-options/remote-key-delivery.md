---
title: 远程和本地iOS密钥投放
description: 远程和本地iOS密钥投放
copied-description: true
exl-id: becc2d3f-39f3-40ee-b980-7dfbbe6f569d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 远程和本地iOS密钥投放 {#remote-and-local-ios-key-delivery}

Adobe Primetime支持将密钥交付到iOS客户端的以下选项：

* **远程**  — 按HTTP实时流(HLS)规范中指定的方式执行；M3U8清单指定了一个HTTPS路径，该路径包含一个AES密钥，该密钥应该用于解密流中的以下加密区段。 当您指定 `Remote` 在Primetime DRM策略中，客户端设备必须连接到远程HTTPS服务器才能获取AES密钥。

* **本地**  — 当您指定 `Local` 在Primetime DRM中，不是连接到Internet/网络来获取AES密钥，而是将本地HTTPS服务器嵌入到iOS应用程序中，然后该服务器管理所有AES密钥请求。 在P应用程序中自动设置和配置嵌入式HTTPS服务器。 应用程序开发人员无需干预。

远程密钥投放通过用于打包内容的Primetime DRM策略启用。 如果要更改此设置，必须重新打包内容。 如果启用了远程密钥投放，则必须部署可以管理来自iOS客户端的密钥请求的Primetime DRM密钥服务器。 但是，对于其他平台上的客户端，工作流没有变化。

>[!NOTE]
>
>密钥投放选择仅影响iOS客户端。 所有其他使用HLS内容的设备，例如Android和桌面版Primetime(Flash Player)，始终使用 `Local` 密钥投放，即使 `Remote` 已指定。
