---
title: 存储凭据
description: 存储凭据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 存储凭据{#storing-credentials}

SDK支持多种存储凭据的方式（公钥证书及其关联的私钥），包括在HSM上或作为PKCS12文件存储。 当需要私钥时（例如，用于打包程序对元数据签名，或者用于许可证服务器对使用许可证服务器或传输公钥加密的数据进行解密），将使用凭据。 必须严格保护私钥以确保您的内容和许可证服务器的安全。 PKCS12是一种标准格式，用于包含使用密码加密的凭据的文件。 文件扩展名.pfx通常用于此格式的文件。

>[!NOTE]
>
>Adobe建议使用HSM以获得最大安全性。 有关详细信息，请参阅Adobe访问安全部署准则。

>[!NOTE]
>
>从Java1.7开始，用于Windows的64位Sun Java不支持Adobe访问DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，请使用32位版本的Java，或使用支持完整PKCS11接口的JDK。

您可以在Hardware Security Module (HSM)上保留私钥，并使用SDK传递从HSM获得的凭据。 要使用存储在HSM上的凭据，请使用可与HSM通信的JCE提供商获取私钥句柄。 然后，将私钥句柄、提供程序名称和包含公钥的证书传递到 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11提供程序是可用于访问HSM上的私钥的JCE提供程序的一个示例（有关使用此提供程序的说明，请参见Sun Java文档）。 某些HSM还随附Java SDK，其中包含JCE提供程序。

PEM和DER是两种编码公钥证书的方法。 PEM是base-64编码，而DER是二进制编码。 证书文件通常使用扩展名.cer、.pem。 或.der. 证书用在只需要公钥的地方。 如果组件仅需要公钥才能操作，则最好为该组件提供证书，而不是凭据或PKCS12文件。
