---
title: 存储凭据
description: 存储凭据
copied-description: true
exl-id: 42bccf3a-307f-4763-8b02-f983bcc2e131
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 存储凭据{#storing-credentials}

SDK支持多种存储凭据的方式（公钥证书及其关联的私钥），包括在HSM上或作为PKCS12文件存储。 当需要私钥时（例如，用于打包员对元数据签名，或用于许可证服务器解密使用许可证服务器或传输公钥加密的数据），将使用凭据。 必须严格保护私钥以确保您的内容和许可证服务器的安全。 PKCS12是文件的标准格式，其中包含使用密码加密的凭据。 文件扩展名.pfx通常用于此格式的文件。

>[!NOTE]
>
>Adobe建议使用HSM以获得最大安全性。 有关详细信息，请参阅Adobe访问安全部署准则。

>[!NOTE]
>
>从Java1.7开始，64位Sun Java for Windows不支持Adobe访问DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，请使用32位版本的Java，或使用支持完整PKCS11接口的JDK。

您可以在Hardware Security Module (HSM)上保留私钥，并使用SDK传递从HSM获得的凭据。 要使用存储在HSM上的凭据，请使用可与HSM通信的JCE提供商获取私钥的句柄。 然后，将私钥句柄、提供程序名称和包含公钥的证书传递到 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11提供程序是可用于访问HSM上的私钥的JCE提供程序的一个示例（有关使用此提供程序的说明，请参阅Sun Java文档）。 某些HSM还随附一个Java SDK，其中包含JCE提供商。

PEM和DER是对公钥证书进行编码的两种方式。 PEM是base-64编码，DER是二进制编码。 证书文件通常使用扩展名.cer、.pem。 或.der. 证书用在只需要公钥的地方。 如果组件仅需要公钥才能操作，则最好为该组件提供证书，而不是凭据或PKCS12文件。
