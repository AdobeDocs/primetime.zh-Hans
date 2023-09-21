---
title: 使用DRM策略更新列表
description: 使用DRM策略更新列表
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# DRM策略更新列表 {#drm-policy-update-lists}

如果在打包任何内容后更新DRM策略中的使用规则，则许可证服务器需要具有最新版本，然后才能颁发使用更新的DRM策略的许可证。 实现此目标的一种方法是通过DRM策略更新列表。

DRM策略更新列表由包括已更新或已撤销DRM策略列表的文件表示。 每当您更新DRM策略时，都需要生成新的DRM策略更新列表并定期将该列表推送到所有许可证服务器。

## 使用DRM策略更新列表 {#working-with-drm-policy-update-lists}

对于无权访问数据库以存储DRM策略信息的许可证服务器，您可能希望使用DRM策略更新列表将任何更新的DRM策略通知许可证服务器。 DRM策略更新列表可能包括DRM策略的更新版本或已撤销的DRM策略ID列表。 如果策略更新列表包含在中 `HandlerConfiguration`，SDK会在颁发许可证时强制实施此列表。

如果内容所有者或分发者希望按照特定的DRM策略停止颁发许可证，您还可以撤销任何DRM策略。 DRM策略更新列表可用于在SDK中强制执行DRM策略吊销。 您还可以应用DRM策略更新列表以向SDK提供已更新DRM策略的列表。

>[!NOTE]
>
>每当您撤销DRM策略时，已颁发的任何许可证都不会自动撤销。 它仅防止根据该DRM政策颁发额外的许可证。

## 更新策略更新列表{#update-policy-update-lists}

使用DRM策略更新列表涉及使用 `PolicyUpdateListFactory` 对象。 如果要创建DRM策略更新列表，则需要加载现有的DRM策略更新列表，然后检查是否已使用Java API更新或撤消DRM策略。

要使用DRM策略更新列表，请执行以下操作：

1. 设置开发环境，并包含在项目中设置开发环境时包含的所有JAR文件。
1. 创建 `ServerCredentialFactory` 用于加载签名所需的凭据的实例。
1. 创建 `PolicyUpdateListFactory` 实例 `ServerCredential` 你创造的。
1. 指定要撤销的DRM策略ID。
1. 创建 `PolicyRevocationEntry` 使用DRM策略ID的对象 `String` 您刚刚创建的，然后通过将其传递到，将其添加到DRM策略更新列表中 `PolicyUpdateListFactory.addRevocationEntry()`.
1. 通过调用生成新的DRM策略更新列表 `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   同样，可以使用将DRM策略更新到列表中 `PolicyUpdateEntry`.
1. 如果DRM策略更新列表已经存在，可以通过调用将其序列化以便加载 `PolicyUpdateList.getBytes()`.

   要加载列表，请调用 `PolicyUpdateListFactory.loadPolicyUpdateList()` 并在序列化列表中传递。
1. 通过调用验证签名是否有效以及列表是否由正确的许可证服务器证书签名 `PolicyUpdateList.verifySignature()`.
1. 传递DRM策略ID `String` 到 `PolicyUpdateList.isRevoked()` 验证条目是否已撤销。

   或者，您可以将列表传递给 `HandlerConfiguration` 在颁发许可证时执行。
如果要向现有条目添加更多条目 `PolicyUpdateList`，则需要加载现有的DRM策略更新列表。 因此，您需要创建新的DRM `PolicyUpdateListFactory` 实例。 调用 `PolicyUpdateListFactory.addEntries` 将旧列表中的所有条目添加到新列表中。 调用 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 向DRM PolicyUpdateList中添加任何新的吊销或更新条目。

有关演示如何创建DRM策略更新列表的示例代码，请参阅 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 在 *参考实施命令行工具* [!DNL samples] 目录。
