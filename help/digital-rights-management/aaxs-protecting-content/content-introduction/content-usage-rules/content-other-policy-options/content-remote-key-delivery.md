---
title: 远程和本地iOS密钥交付
description: 远程和本地iOS密钥交付
copied-description: true
exl-id: de9c7070-46a9-453c-9d98-a9f161282cfa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 远程和本地iOS密钥交付{#remote-and-local-ios-key-delivery}

Adobe Primetime支持将密钥交付到iOS客户端的两个选项：

* Remote - M3U8清单指定了一个HTTPS路径，该路径包含一个AES密钥，应该用于解密流中的以下加密段，与HLS规范中指定的完全相同。 当指定“远程”时，客户端设备将联系远程HTTPS服务器以获取AES密钥。
* 本地 — 当指定“本地”时，本地HTTPS服务器将嵌入到iOS应用程序中，该应用程序将处理所有AES密钥请求，而不是通过Internet/网络访问AES密钥。 在Primetime应用程序中自动设置和配置嵌入式HTTPS服务器。 应用程序开发人员无需干预。

通过用于打包内容的策略启用远程密钥投放（更改此设置要求对内容重新打包）。启用远程密钥投放时，必须部署Adobe访问密钥服务器来处理来自iOS客户端的密钥请求，但不会更改其他平台上客户端的工作流。

>[!NOTE]
>
>密钥投放选择仅影响iOS客户端。 使用HLS内容的所有其他设备将始终使用“本地”密钥投放，即使已指定“远程”也是如此。

有关信息，请参阅 *使用Adobe访问密钥服务器*.
