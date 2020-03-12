---
seo-title: 远程和本地iOS密钥交付
title: 远程和本地iOS密钥交付
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 远程和本地iOS密钥交付{#remote-and-local-ios-key-delivery}

Adobe Primetime支持两种关键交付到iOS客户端的选项：

* 远程——正如在HLS规范中指定的，M3U8清单指定的HTTPS路径包含AES密钥，该密钥应用于解密流中的以下加密段。 指定“远程”时，客户端设备将连接到远程HTTPS服务器以获取AES密钥。
* 本地——当指定“本地”时，本地HTTPS服务器将嵌入到iOS应用程序中，该应用程序将处理所有AES密钥请求，而不是通过Internet/网络访问AES密钥。 嵌入式HTTPS服务器在Primetime应用程序中自动设置和配置。 应用程序开发人员无需干预。

通过用于打包内容的策略启用远程密钥交付（更改此设置需要重新打包内容），启用远程密钥交付后，必须部署Adobe Access Key Server，以处理来自iOS客户端的密钥请求，但对于其他平台上的客户端的工作流程没有更改。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>密钥交付选择仅影响iOS客户端。 使用HLS内容的所有其他设备将始终使用“本地”密钥交付，即使已指定“远程”。

有关信息，请参 *阅使用Adobe Access Key Server*。
