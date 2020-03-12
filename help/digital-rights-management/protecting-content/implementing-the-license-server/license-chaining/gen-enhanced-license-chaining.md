---
seo-title: 增强的许可证链接
title: 增强的许可证链接
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 增强的许可证链接 {#enhanced-license-chaining}

如果使用DRM策略生成支持许可证链接的许可证，则服务器必须决定是发布Leaf许可证、根许可证还是同时发布两者。 如果要确定DRM策略支持的许可证链接类型，则必须使用或 `Policy.getLicenseChainType()`致电确定 `Policy.getRootLicenseId()` DRM策略是否具有根许可证。 通过Adobe Primetime DRM 2.0许可证链接，服务器通常在用户首次请求特定计算机的许可证时发出叶许可证，此后发出根许可证。 如果要确定计算机是否已具有指定策略的叶许可证，您需要调用 `LicenseRequestMessage.clientHasLeafForPolicy()`。

借助Adobe Primetime DRM 3.0中增强的许可证链接，建议用户在首次请求特定计算机的许可证时同时发布Leaf和Root。 如果用户已拥有根许可证，则服务器可能只发出Leaf(调 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 用以确定客户端是否已拥有3.0增强的根)。 对于后续的许可证请求，客户端随后会指示它已有Leaf和Root，因此服务器应发布新的Root许可证。 当使用增强的许可证链时， `setRootKeyRetrievalInfo()` 必须调用以提供在DRM策略中解密根加密密钥所需的凭据。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果策略支持3.0增强许可证链接，但客户端是Primetime DRM 2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用 `LicenseRequestMessage.getClientVersion()`。

