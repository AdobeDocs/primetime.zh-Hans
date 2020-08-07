---
seo-title: 增强的许可证链接
title: 增强的许可证链接
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 增强的许可证链接 {#enhanced-license-chaining}

借助AdobeAccess 3.0中增强的许可证链接，建议用户在首次请求特定计算机的许可证时同时发布Leaf和Root。 如果用户已拥有根许可证，则服务器可能仅发出Leaf( `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 调用以确定客户端是否已具有3.0增强根)。 对于后续的许可证请求，客户端将指示它已具有Leaf和Root，因此服务器应发布新的Root许可证。 使用增强的许可证链时， `setRootKeyRetrievalInfo()` 必须调用以提供解密策略中的根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强许可证链接，但客户端是Adobe访问2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用LicenseRequestMessage.getClientVersion()。

