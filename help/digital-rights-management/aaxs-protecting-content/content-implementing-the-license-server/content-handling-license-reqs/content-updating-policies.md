---
seo-title: 更新策略
title: 更新策略
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 更新策略{#updating-policies}

如果在打包内容后更新策略，请向许可证服务器提供更新的策略，以便在发布许可证时使用更新的版本。 如果您的许可证服务器有权访问存储策略的数据库，则可以从数据库检索更新的策略并调用`LicenseRequestMessage.setSelectedPolicy()`提供新版本的策略。

对于不依赖中央数据库的许可证服务器，SDK提供对策略更新列表的支持。 策略更新列表是包含已更新或已吊销策略列表的文件。 更新策略时，生成新的策略更新列表，并定期将列表推送到所有许可证服务器。 通过设置`HandlerConfiguration.setPolicyUpdateList()`将列表传递给SDK。 如果提供了更新列表，则SDK在解析内容元数据时会咨询此列表。 `ContentInfo.getUpdatedPolicies()` 包含元数据中指定的策略的更新版本。

请参阅[使用策略](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)和[策略更新列表。](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
