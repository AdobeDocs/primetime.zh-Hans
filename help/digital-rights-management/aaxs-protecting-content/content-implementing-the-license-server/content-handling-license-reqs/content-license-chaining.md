---
seo-title: 许可证链接
title: 许可证链接
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证链接{#license-chaining}

如果用于生成许可证的策略支持许可证链接，则服务器必须决定是发布Leaf许可证、Root许可证还是同时发布两者。 要确定策略支持的许可证链接类型，请使 `Policy.getLicenseChainType()`用或调用来确 `Policy.getRootLicenseId()` 定策略是否具有根许可证。 通过Adobe Access 2.0许可证链接，服务器通常在用户第一次请求特定计算机的许可证时颁发叶许可证，此后再颁发根许可证。 要确定计算机是否已具有指定策略的叶许可证，请调用 `LicenseRequestMessage.clientHasLeafForPolicy()`。
