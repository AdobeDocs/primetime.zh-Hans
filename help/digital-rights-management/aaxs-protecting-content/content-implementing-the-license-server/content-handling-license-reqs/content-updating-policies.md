---
title: 更新策略
description: 更新策略
copied-description: true
exl-id: 0ea8d03b-68dd-415e-a75b-fd439bf858b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 更新策略 {#updating-policies}

如果策略在内容打包后更新，请将更新的策略提供给许可证服务器，以便在颁发许可证时可以使用更新的版本。 如果您的许可证服务器可以访问数据库来存储策略，则可以从数据库中检索更新的策略并调用 `LicenseRequestMessage.setSelectedPolicy()` 提供策略的新版本。

对于不依赖中央数据库的许可证服务器，SDK提供对策略更新列表的支持。 策略更新列表是包含已更新或已撤消策略列表的文件。 更新策略时，生成新的策略更新列表，并定期将该列表推送到所有许可证服务器。 通过设置将列表传递到SDK `HandlerConfiguration.setPolicyUpdateList()`. 如果提供了更新列表，则SDK在解析内容元数据时会参考此列表。 `ContentInfo.getUpdatedPolicies()` 包含元数据中指定的策略的更新版本。

参见 [使用策略](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) 和 [策略更新列表。](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
