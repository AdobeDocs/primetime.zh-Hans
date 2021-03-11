---
title: 许可证链接
description: 许可证链接
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 许可证链{#license-chaining}

如果用于生成许可证的策略支持许可证链接，则服务器必须决定是发放Leaf许可证、Root许可证还是同时发放两者。 要确定策略所支持的许可证链接类型，请使用`Policy.getLicenseChainType()`或调用`Policy.getRootLicenseId()`确定策略是否具有根许可证。 通过Adobe Access 2.0许可证链，服务器通常在用户第一次请求特定计算机的许可证时发出叶许可证，随后发出根许可证。 要确定计算机是否已具有指定策略的叶许可证，请调用`LicenseRequestMessage.clientHasLeafForPolicy()`。
