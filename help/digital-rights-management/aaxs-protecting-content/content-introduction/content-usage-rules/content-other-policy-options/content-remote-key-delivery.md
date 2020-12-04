---
seo-title: 远程和本地iOS密钥投放
title: 远程和本地iOS密钥投放
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# 远程和本地iOS密钥投放{#remote-and-local-ios-key-delivery}

Adobe Primetime支持两种iOS客户端关键投放选项：

* 远程——正如HLS规范中指定的，M3U8清单指定了HTTPS路径，该路径包含AES密钥，该密钥应用于解密流中的以下加密段。 指定“Remote”时，客户端设备将连接到远程HTTPS服务器以获取AES密钥。
* 本地——当指定“本地”时，本地HTTPS服务器将嵌入到iOS应用程序中，iOS应用程序将处理所有AES密钥请求，而不是通过Internet/网络访问AES密钥。 嵌入式HTTPS服务器在Primetime应用程序中自动设置和配置。 应用程序开发者无需任何干预。

远程密钥投放通过用于打包内容的策略启用（更改此设置需要重新打包内容），启用远程密钥投放后，必须部署Adobe访问密钥服务器来处理来自iOS客户端的密钥请求，但对其他平台上的客户端的工作流没有更改。

>[!NOTE]
>
>“关键投放”选择仅影响iOS客户端。 使用HLS内容的所有其他设备将始终使用“本地”密钥投放，即使已指定“远程”。

有关信息，请参阅&#x200B;*使用Adobe访问密钥服务器*。
