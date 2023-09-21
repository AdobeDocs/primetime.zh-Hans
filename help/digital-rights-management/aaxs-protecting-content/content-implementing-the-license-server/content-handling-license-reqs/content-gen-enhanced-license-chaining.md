---
title: 增强型许可证链接
description: 增强型许可证链接
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 增强型许可证链接 {#enhanced-license-chaining}

通过Adobe访问3.0中的增强许可证链接，建议在用户首次请求特定计算机的许可证时同时颁发Leaf和Root。 如果用户已经拥有Root许可证，则服务器只能发出Leaf(调用 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 以确定客户端是否已具有3.0 Enhanced Root)。 对于后续许可证请求，客户端将指示它已经具有叶和根，因此服务器应颁发新的根许可证。 当使用增强型许可证链接时， `setRootKeyRetrievalInfo()` 必须调用以提供在策略中解密根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强型许可证链接，但客户端AdobeAccess 2.0，则服务器将颁发2.0原始链接许可证。 要确定客户端版本，请使用LicenseRequestMessage.getClientVersion()。
