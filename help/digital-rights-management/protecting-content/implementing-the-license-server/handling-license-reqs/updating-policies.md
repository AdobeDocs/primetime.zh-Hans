---
title: 更新DRM策略
description: 更新DRM策略
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 更新DRM策略 {#updating-drm-policies}

如果在封装内容后更新DRM策略，则向许可证服务器提供更新的DRM策略，以便在颁发许可证时可以使用更新的版本。 如果许可证服务器可以访问用于存储DRM策略的数据库，则可以从数据库中检索更新的DRM策略并调用 `LicenseRequestMessage.setSelectedPolicy()` 提供DRM策略的新版本。

对于不依赖中央数据库的许可证服务器，SDK支持DRM策略更新列表。 DRM策略更新列表是包含已更新或已撤销DRM策略列表的文件。 更新DRM策略时，生成新的DRM策略更新列表并定期将该列表推送到所有许可证服务器。 通过设置将列表传递到SDK `HandlerConfiguration.setPolicyUpdateList()`. 如果提供了更新列表，则SDK在解析内容元数据时会参考此列表。 `ContentInfo.getUpdatedPolicies()` 包括元数据中指定的DRM策略的更新版本。

请参阅 [使用DRM策略](../../../protecting-content/working-policies-overview/working-with-policies.md) 和 [DRM策略更新列表](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
