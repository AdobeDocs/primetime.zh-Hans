---
seo-title: 使用策略更新列表
title: 使用策略更新列表
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用策略更新列表{#working-with-policy-update-lists}

对于无权访问数据库以存储有关策略的信息的许可证服务器，您可能希望使用策略更新列表向许可证服务器通知已更新的策略。 策略更新列表可能包含已撤销的策略的更新版本或策略ID列表。 如果中提供了策略更新列 `HandlerConfiguration`表，则SDK将在发布许可证时强制执行此列表。

如果内容所有者或分发者希望根据特定策略停止发行许可证，则也可撤销这些政策。 策略更新列表可用于在SDK中强制执行策略撤销。 策略更新列表还可用于向SDK提供更新策略的列表。 请注意，撤销策略不会撤销已发布的许可证。 它只会阻止根据该政策发行其他许可证。

使用策略更新列表涉及对象的使 `PolicyUpdateListFactory` 用。 要创建策略更新列表，请加载现有策略更新列表，并使用Java API检查策略是已更新还是已吊销，请执行以下步骤：

1. 设置开发环境并包含项目中设置开发环境中提到的所有JAR文件。
1. 创建一 `ServerCredentialFactory` 个实例以加载签名所需的凭据。
1. 使用您 `PolicyUpdateListFactory` 创建的实例 `ServerCredential` 创建实例。
1. 指定要撤销的策略ID。
1. 使用您 `PolicyRevocationEntry` 刚创建的策略ID创建 `String` 一个对象，并将其传入策略更新列表，将其添加到策略更新列表 `PolicyUpdateListFactory.addRevocationEntry()`。 通过调用生成新策略更新列表 `PolicyUpdateListFactory.generatePolicyUpdateList()`。 同样，更新的策略也可以使用添加到列表 `PolicyUpdateEntry`。
1. 如果策略更新列表已存在，则可以通过调用对其进行序列化以进行加载 `PolicyUpdateList.getBytes()`。 要加载列表，请调 `PolicyUpdateListFactory.loadPolicyUpdateList()` 用并传入序列化列表。
1. 通过调用验证签名是否有效以及列表是否已由正确的许可证服务器证书进行签名 `PolicyUpdateList.verifySignature()`。
1. 要检查某个条目是否被撤销，请将策略ID传 `String` 递到 `PolicyUpdateList.isRevoked()`。 或者，该列表可以传入，并 `HandlerConfiguration` 且在发放许可证时强制执行。

要向现有策略添加其他条目， `PolicyUpdateList`请加载现有策略更新列表。 创建新实 `PolicyUpdateListFactory` 例。 调用P `olicyUpdateListFactory.addEntries` 将旧列表中的所有条目添加到新列表。 调用 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 将任何新的撤销或更新条目添加到PolicyUpdateList。

有关演示如何创建策略更新列表、加载现有策略更新列表以及检查策略是否已吊销的示例代码，请参阅 `com.adobe.flashaccess.samples.policyupdatelist``.CreatePolicyUpdateList` Reference Implementation Command Line Tools &quot;samples&quot;目录中的策略。
