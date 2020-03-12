---
seo-title: 存储凭据
title: 存储凭据
uuid: dbce523c-32d9-423f-bc95-39786f85fc29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 存储凭据{#storing-credentials}

SDK支持多种存储凭据（公钥证书及其关联的私钥）的方式，包括在HSM上或作为PKCS12文件。 在需要私钥时使用凭据（例如，包装程序对元数据进行签名，或许可证服务器解密使用许可证服务器或传输公钥加密的数据）。 私钥必须受到严密保护，以确保您的内容和许可证服务器的安全。 PKCS12是一种标准格式，用于包含使用密码加密的凭证的文件。 文件扩展名。pfx通常用于此格式的文件。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe建议使用HSM以获得最大的安全性。 有关详细信息，请参阅Adobe Access安全部署准则。

>[!NOTE] {importance=&quot;high&quot;}
>
>从Java1.7开始，64位Sun Java for Windows不支持Adobe Access DRM为与HSM设备通信而需要的PKCS11接口。 如果您计划使用HSM，请使用32位版本的Java，或使用支持完整PKCS11接口的JDK。

您可以在硬件安全模块(HSM)上保留私钥，并使用SDK传递您从HSM获得的凭证。 要使用存储在HSM上的凭据，请使用可与HSM通信的JCE提供程序来处理私钥。 然后，将私钥句柄、提供者名称和包含公钥的证书传递给 `ServerCredentialFactory.getServerCredential()`。

SunPKCS11提供程序是JCE提供程序的一个示例，它可用于访问HSM上的私钥（有关使用此提供程序的说明，请参阅Sun Java文档）。 某些HSM还附带Java SDK，其中包括JCE提供程序。

PEM和DER是对公钥证书进行编码的两种方式。 PEM是基本64编码，DER是二进制编码。 证书文件通常使用扩展名。cer、.pem。 或。der。 证书仅在需要公钥的位置使用。 如果组件仅需要公钥才能运行，则最好为该组件提供证书，而不是凭据或PKCS12文件。
