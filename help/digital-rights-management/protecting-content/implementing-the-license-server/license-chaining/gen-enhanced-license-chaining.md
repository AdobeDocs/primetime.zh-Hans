---
title: 增强的许可证链接
description: 增强的许可证链接
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 增强的许可证链{#enhanced-license-chaining}

如果使用DRM策略生成支持许可证链接的许可证，则服务器必须决定是发放叶许可证、根许可证还是同时发放两者。 如果要确定DRM策略支持的许可证链接类型，则必须使用`Policy.getLicenseChainType()`或调用`Policy.getRootLicenseId()`来确定DRM策略是否具有根许可证。 借助Adobe Primetime DRM 2.0许可证链，服务器通常在用户第一次请求特定计算机的许可证时发出叶许可证，此后发出根许可证。 如果要确定计算机是否已具有指定策略的叶许可证，则需要调用`LicenseRequestMessage.clientHasLeafForPolicy()`。

借助Adobe Primetime DRM 3.0中增强的许可证链接，建议用户在第一次请求特定计算机的许可证时同时发布叶和根。 如果用户已拥有Root许可证，则服务器可能仅发出Leaf（调用`LicenseRequestMessage.clientHasEnhancedRootForPolicy()`以确定客户端是否已拥有3.0 Enhanced Root）。 然后，对于后续的许可证请求，客户端会指示它已具有Leaf和Root，因此服务器应发布新的Root许可证。 当使用增强的许可证链时，必须调用`setRootKeyRetrievalInfo()`以提供解密DRM策略中的根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强许可证链接，但客户端是Primetime DRM 2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用`LicenseRequestMessage.getClientVersion()`。

