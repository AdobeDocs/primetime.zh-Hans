---
title: 使用策略更新列表
description: 使用策略更新列表
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# 使用策略更新列表{#working-with-policy-update-lists}

对于无法访问数据库以存储有关策略信息的许可证服务器，您可能希望使用策略更新列表将已更新的策略通知许可证服务器。 策略更新列表可能包含更新版本的策略或已撤消的策略ID列表。 如果策略更新列表提供于 `HandlerConfiguration`，SDK将在颁发许可证时强制实施此列表。

如果内容所有者或分发者希望按照特定策略停止颁发许可证，策略也可以撤销。 策略更新列表可用于在SDK中强制实施策略吊销。 策略更新列表也可用于向SDK提供已更新策略的列表。 请注意，撤销策略不会撤销已颁发的许可证。 它只会阻止根据该策略颁发额外的许可证。

使用策略更新列表涉及使用 `PolicyUpdateListFactory` 对象。 要创建策略更新列表，加载现有的策略更新列表，并使用Java API检查策略是否已更新或撤销，请执行以下步骤：

1. 设置开发环境，并将设置开发环境中所述的所有JAR文件包含在项目中。
1. 创建 `ServerCredentialFactory` 用于加载签名所需的凭据的实例。
1. 创建 `PolicyUpdateListFactory` 实例使用 `ServerCredential` 您已创建。
1. 指定要撤消的策略ID。
1. 创建 `PolicyRevocationEntry` 使用策略ID的对象 `String` 您刚刚创建了，并将其传递到以将它添加到策略更新列表 `PolicyUpdateListFactory.addRevocationEntry()`. 通过调用生成新的策略更新列表 `PolicyUpdateListFactory.generatePolicyUpdateList()`. 同样，可以使用将更新的策略添加到列表中 `PolicyUpdateEntry`.
1. 如果策略更新列表已存在，您可以通过调用将其序列化以供加载 `PolicyUpdateList.getBytes()`. 要加载列表，请调用 `PolicyUpdateListFactory.loadPolicyUpdateList()` 并在序列化列表中传递。
1. 通过调用，验证签名是否有效，以及列表是否由正确的许可证服务器证书签名 `PolicyUpdateList.verifySignature()`.
1. 要检查条目是否被撤销，请传递策略ID `String` 到 `PolicyUpdateList.isRevoked()`. 或者，可以将列表传递到 `HandlerConfiguration` 在颁发许可证时强制执行。

向现有条目添加附加条目 `PolicyUpdateList`，加载现有策略更新列表。 新建 `PolicyUpdateListFactory` 实例。 呼叫P `olicyUpdateListFactory.addEntries` 将旧列表中的所有条目添加到新列表中。 调用 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 向PolicyUpdateList中添加任何新的吊销或更新条目。

有关演示如何创建策略更新列表、加载现有策略更新列表以及检查策略是否已被撤销的示例代码，请参阅 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 在参考实施命令行工具“samples”目录中。
