---
title: 增强的许可证链接
description: 增强的许可证链接
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 增强的许可证链{#enhanced-license-chaining}

借助Adobe Access 3.0中增强的许可证链接，建议用户在第一次请求特定计算机的许可证时同时发布Leaf和Root。 如果用户已拥有Root许可证，则服务器可能仅发出Leaf（调用`LicenseRequestMessage.clientHasEnhancedRootForPolicy()`以确定客户端是否已拥有3.0 Enhanced Root）。 对于后续的许可证请求，客户端将指示它已具有Leaf和Root，因此服务器应发布新的Root许可证。 当使用增强的许可证链时，必须调用`setRootKeyRetrievalInfo()`以提供解密策略中的根加密密钥所需的凭据。

>[!NOTE]
>
>如果策略支持3.0增强许可证链接，但客户端是Adobe Access 2.0，则服务器将发出2.0原始链接许可证。 要确定客户端版本，请使用LicenseRequestMessage.getClientVersion()。

