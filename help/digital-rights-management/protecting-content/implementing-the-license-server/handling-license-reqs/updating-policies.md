---
seo-title: 更新DRM策略
title: 更新DRM策略
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 更新DRM策略{#updating-drm-policies}

如果在打包内容后更新了DRM策略，则向许可证服务器提供更新的DRM策略，以便在发放许可证时可以使用更新的版本。 如果许可证服务器有权访问存储DRM策略的数据库，则可以从数据库检索更新的DRM策略，并调用`LicenseRequestMessage.setSelectedPolicy()`提供DRM策略的新版本。

对于不依赖中央数据库的许可证服务器，SDK提供对DRM策略更新列表的支持。 DRM策略更新列表是包含已更新或已撤销DRM策略的列表的文件。 更新DRM策略时，生成新的DRM策略更新列表，并定期将列表推送到所有许可证服务器。 通过设置`HandlerConfiguration.setPolicyUpdateList()`将列表传递给SDK。 如果提供了更新列表，则SDK在解析内容元数据时会咨询此列表。 `ContentInfo.getUpdatedPolicies()` 包括元数据中指定的DRM策略的更新版本。

请参阅[使用DRM策略](../../../protecting-content/working-policies-overview/working-with-policies.md)和[DRM策略更新列表](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)