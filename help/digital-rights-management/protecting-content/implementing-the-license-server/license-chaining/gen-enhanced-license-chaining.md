---
seo-title: 增强的许可证链接
title: 增强的许可证链接
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 增强的许可证链接 {#enhanced-license-chaining}

如果DRM策略用于生成支持许可证链接的许可证，则服务器必须决定是发放Leaf许可证、根许可证还是同时发放两者。 如果要确定DRM策略支持的许可证链接类型，则必须使用或 `Policy.getLicenseChainType()`致电确 `Policy.getRootLicenseId()` 定DRM策略是否具有根许可证。 使用Adobe PrimetimeDRM 2.0许可证链，服务器通常在用户第一次请求特定机器的许可证时颁发叶许可证，此后颁发根许可证。 如果要确定计算机是否已具有指定策略的叶许可证，您需要调用 `LicenseRequestMessage.clientHasLeafForPolicy()`。

借助Adobe PrimetimeDRM 3.0中增强的许可证链接，建议用户在首次请求特定计算机的许可证时同时发布Leaf和Root。 如果用户已拥有根许可证，则服务器可能仅发出Leaf( `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 调用以确定客户端是否已具有3.0增强根)。 对于后续的许可证请求，客户端随后会指示它已具有Leaf和Root，因此服务器应发布新的Root许可证。 当使用增强的许可证链时， `setRootKeyRetrievalInfo()` 必须调用以提供在DRM策略中解密根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强许可证链接，但客户端是Primetime DRM 2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用 `LicenseRequestMessage.getClientVersion()`。

