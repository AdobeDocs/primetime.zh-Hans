---
seo-title: 存储凭据
title: 存储凭据
uuid: a9e9db72-c921-4c28-ad1d-3fd3c2283f14
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# 存储凭据{#storing-credentials}

Primetime DRM SDK支持存储凭据的不同方式，包括使用硬件安全模块(HSM)或作为PKCS12文件。 当需要私钥时，SDK会使用凭据（公钥证书和关联的私钥）。 例如，包装程序使用凭据对元数据进行签名；许可证服务器使用凭据解密已使用许可证服务器或传输公钥加密的数据。

您必须密切保护私钥，以确保内容和许可证服务器的安全。 PKCS12是存储已使用密码加密的凭据的标准存档文件格式。 （您还可以加密PKCS12文件并对其进行签名。） 文件扩展名[!DNL .pfx]通常用于支持此格式的文件。

>[!NOTE]
>
>Adobe建议您使用HSM来实现最高安全性。
>
>请参阅&#x200B;*Adobe PrimetimeDRM安全部署指南*。

>[!NOTE]
>
>自Java 1.7起，64位Sun Java for Windows不再支持Primetime DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，则需要使用32位版本的Java，或使用支持完整PKCS11接口的JDK。

您可以在HSM上保留私钥，并使用Primetime DRM SDK来传递您从HSM获得的凭据。 如果要使用存储在HSM上的凭据，则需要使用能够与HSM通信的JCE提供程序来处理私钥。 然后，您需要将私钥句柄、提供者名称和包含公钥的证书传递给`ServerCredentialFactory.getServerCredential()`。

SunPKCS11提供程序代表JCE提供程序的一个示例，您可以使用它访问HSM上的私钥。 某些HSM还包含在与JCE提供程序绑定的Java SDK中。

有关如何使用此提供程序的说明，请参阅Sun Java文档。

PEM和DER是对公钥证书进行编码的方式。 PEM是基于64的编码，DER是二进制编码。 证书文件通常使用扩展名[!DNL .cer]、[!DNL .pem]或[!DNL .der]。 仅需要公钥时使用证书。 如果组件仅需要公钥才能运行，建议您为该组件提供证书，而不是凭据或PKCS12文件。
