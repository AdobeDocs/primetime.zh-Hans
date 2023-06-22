---
title: 增强型许可证链接
description: 增强型许可证链接
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 增强型许可证链接 {#enhanced-license-chaining}

通过Adobe访问3.0中增强的许可证链接，建议在用户首次请求特定计算机的许可证时同时颁发叶和根。 如果用户已经拥有Root许可证，则服务器可能只发出叶(调用 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 以确定客户端是否已具有3.0 Enhanced Root)。 对于后续的许可证请求，客户端将指示它已经具有叶和根，因此服务器应颁发一个新的根许可证。 当使用增强型许可证链时， `setRootKeyRetrievalInfo()` 必须调用以提供在策略中解密根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强型许可证链接，但客户端是Adobe访问2.0，则服务器将颁发2.0原始链接许可证。 要确定客户端版本，请使用LicenseRequestMessage.getClientVersion()。
