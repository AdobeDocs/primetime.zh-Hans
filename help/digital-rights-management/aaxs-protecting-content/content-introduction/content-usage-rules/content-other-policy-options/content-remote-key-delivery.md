---
title: 远程和本地iOS密钥交付
description: 远程和本地iOS密钥交付
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 远程和本地iOS密钥交付{#remote-and-local-ios-key-delivery}

Adobe Primetime支持两种将密钥交付到iOS客户端的选项：

* 远程 — 与HLS规范中指定的完全相同，M3U8清单指定了一个HTTPS路径，该路径包含用于解密流中以下加密段的AES密钥。 当指定“远程”时，客户端设备将联系远程HTTPS服务器以获取AES密钥。
* 本地 — 当指定“本地”时，本地HTTPS服务器将嵌入到iOS应用程序中，该应用程序将处理所有AES密钥请求，而不是通过Internet/网络访问AES密钥。 在Primetime应用程序中自动设置和配置嵌入式HTTPS服务器。 应用程序开发人员无需干预。

通过用于打包内容的策略启用远程密钥投放（更改此设置需要对内容重新打包），在启用远程密钥投放时，必须部署Adobe访问密钥服务器来处理来自iOS客户端的密钥请求，但其他平台上的客户端的工作流不会发生更改。

>[!NOTE]
>
>密钥投放选择仅影响iOS客户端。 所有使用HLS内容的其他设备将始终使用“本地”密钥投放，即使已指定“远程”也是如此。

有关信息，请参阅 *使用Adobe访问密钥服务器*.
