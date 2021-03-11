---
title: 更新策略
description: 更新策略
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 更新策略{#updating-policies}

如果在打包内容后更新了策略，请向许可证服务器提供更新的策略，以便在发布许可证时可以使用更新的版本。 如果您的许可证服务器有权访问存储策略的数据库，则可以从数据库检索更新的策略并调用`LicenseRequestMessage.setSelectedPolicy()`以提供策略的新版本。

对于不依赖中央数据库的许可证服务器，SDK提供对策略更新列表的支持。 策略更新列表是包含已更新或已吊销策略列表的文件。 更新策略时，生成新的策略更新列表，并定期将列表推出到所有许可证服务器。 通过设置`HandlerConfiguration.setPolicyUpdateList()`将列表传递到SDK。 如果提供了更新列表，则SDK在分析内容元数据时会咨询此列表。 `ContentInfo.getUpdatedPolicies()` 包含元数据中指定的策略的更新版本。

请参阅[使用策略](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)和[策略更新列表。](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
