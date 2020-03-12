---
seo-title: 更新DRM策略
title: 更新DRM策略
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754

---


# 更新DRM策略 {#updating-drm-policies}

如果在打包内容后更新了DRM策略，则向许可证服务器提供更新的DRM策略，以便在发布许可证时可以使用更新的版本。 如果许可证服务器可以访问存储DRM策略的数据库，则可以从数据库检索更新的DRM策略，并调 `LicenseRequestMessage.setSelectedPolicy()` 用以提供DRM策略的新版本。

对于不依赖中央数据库的许可证服务器，SDK提供对DRM策略更新列表的支持。 DRM策略更新列表是包含已更新或已撤销的DRM策略列表的文件。 更新DRM策略后，生成新的DRM策略更新列表，并定期将该列表推送到所有许可证服务器。 通过设置将列表传递给SDK `HandlerConfiguration.setPolicyUpdateList()`。 如果提供了更新列表，则SDK在分析内容元数据时会咨询此列表。 `ContentInfo.getUpdatedPolicies()` 包括在元数据中指定的DRM策略的更新版本。

请参 [阅使用DRM策略](../../../protecting-content/working-policies-overview/working-with-policies.md) 和 [DRM策略更新列表](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)