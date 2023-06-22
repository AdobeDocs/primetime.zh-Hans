---
title: 存储凭据
description: 存储凭据
copied-description: true
exl-id: ceb1bc19-56a0-47ce-affd-ce4ecb896c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 存储凭据{#storing-credentials}

Primetime DRM SDK支持存储凭据的不同方式，包括使用Hardware Security Module (HSM)或作为PKCS12文件。 当需要私钥时，SDK会使用凭据（公钥证书和关联的私钥）。 例如，打包程序使用凭据对元数据进行签名；许可证服务器使用凭据解密已使用License Server或Transport公钥加密的数据。

您必须严格保护私钥，以确保内容和License Server的安全。 PKCS12是一种标准存档文件格式，用于存储已使用密码加密的凭据。 （您还可以对PKCS12文件本身进行加密和签名。） 文件扩展名 [!DNL .pfx] 通常用于支持此格式的文件。

>[!NOTE]
>
>Adobe建议您使用HSM以获得最大安全性。
>
>请参阅 *Adobe Primetime DRM安全部署准则* 指南。

>[!NOTE]
>
>从Java 1.7开始，64位Sun Java for Windows不再支持Primetime DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，则需要使用32位版本的Java，或使用支持完整PKCS11接口的JDK。

您可以在HSM上保留私钥，并使用Primetime DRM SDK传递从HSM获得的凭据。 如果要使用存储在HSM上的凭据，则需要使用可与HSM通信的JCE提供商获取私钥的句柄。 然后，您需要将私钥句柄、提供程序名称和包含公钥的证书传递到 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11提供程序表示可用于访问HSM上的私钥的JCE提供程序的一个示例。 某些HSM还包含在Java SDK中，该工具与JCE提供商捆绑在一起。

有关如何使用此提供程序的说明，请参见Sun Java文档。

PEM和DER是对公钥证书进行编码的方法。 PEM是base-64编码，DER是二进制编码。 证书文件通常使用扩展名 [!DNL .cer]， [!DNL .pem]，或 [!DNL .der]. 证书用于只需要公钥的情况。 如果组件仅需要公钥才能运行，建议您为该组件提供证书，而不是凭据或PKCS12文件。
