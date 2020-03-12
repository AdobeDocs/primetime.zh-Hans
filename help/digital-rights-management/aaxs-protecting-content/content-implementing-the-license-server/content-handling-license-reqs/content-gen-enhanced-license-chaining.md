---
seo-title: 增强的许可证链接
title: 增强的许可证链接
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: da8736769f7b47318dbd955aa854f83ae64d6d7b

---


# 增强的许可证链接 {#enhanced-license-chaining}

借助Adobe Access 3.0中增强的许可证链接，建议用户在首次请求特定计算机的许可证时同时发布Leaf和Root。 如果用户已拥有根许可证，则服务器可能只发出Leaf(调 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 用以确定客户端是否已拥有3.0增强的根)。 对于后续的许可证请求，客户端将指示它已有Leaf和Root，因此服务器应发布新的Root许可证。 使用增强的许可证链时，必 `setRootKeyRetrievalInfo()` 须调用以提供解密策略中的根加密密钥所需的凭据。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果策略支持3.0增强许可证链接，但客户端是Adobe Access 2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用LicenseRequestMessage.getClientVersion()。

