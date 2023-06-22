---
title: 增强型许可证链接
description: 增强型许可证链接
copied-description: true
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 增强型许可证链接 {#enhanced-license-chaining}

如果DRM策略用于生成支持许可证链接的许可证，则服务器必须决定是颁发叶许可证、根许可证，还是同时颁发两者。 如果要确定DRM策略支持的许可证链接类型，则必须使用 `Policy.getLicenseChainType()`，或调用 `Policy.getRootLicenseId()` 确定DRM策略是否具有根许可证。 通过Adobe Primetime DRM 2.0许可证链接，服务器通常在用户首次请求特定计算机的许可证时发出叶许可证，此后发出根许可证。 如果要确定计算机是否已具有指定策略的叶许可证，则需要调用 `LicenseRequestMessage.clientHasLeafForPolicy()`.

通过Adobe Primetime DRM 3.0中的增强型许可证链接，建议在用户首次请求特定计算机的许可证时同时颁发叶和根。 如果用户已经拥有Root许可证，则服务器可能只发出叶(调用 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 以确定客户端是否已具有3.0 Enhanced Root)。 对于后续的许可证请求，客户端会指示它已经具有叶和根，因此服务器应颁发新的根许可证。 当使用增强型许可证链时， `setRootKeyRetrievalInfo()` 必须调用以提供在DRM策略中解密根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强型许可证链接，但客户端是Primetime DRM 2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用 `LicenseRequestMessage.getClientVersion()`.
