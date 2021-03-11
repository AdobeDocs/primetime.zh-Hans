---
title: 使用策略更新列表
description: 使用策略更新列表
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# 使用策略更新列表{#working-with-policy-update-lists}

对于无权访问数据库以存储有关策略的信息的许可证服务器，您可能希望使用策略更新列表向许可证服务器通知已更新的策略。 “策略更新”列表可能包含已吊销的策略的更新版本或策略ID的列表。 如果`HandlerConfiguration`中提供了策略更新列表，则SDK将在颁发许可证时强制执行此列表。

如果内容所有者或分销商希望根据特定政策停止发行许可证，则也可撤销策略。 策略更新列表可用于在SDK中强制策略吊销。 策略更新列表也可用于向SDK提供更新策略的列表。 请注意，撤销策略不会撤销已颁发的许可证。 它只会阻止根据该政策颁发额外的许可证。

使用策略更新列表涉及使用`PolicyUpdateListFactory`对象。 要创建策略更新列表，请加载现有策略更新列表，并使用Java API检查策略是否已更新或吊销，请执行以下步骤：

1. 设置开发环境，并包含项目中设置开发环境中提到的所有JAR文件。
1. 创建一个`ServerCredentialFactory`实例以加载签名所需的凭据。
1. 使用您创建的`ServerCredential`创建`PolicyUpdateListFactory`实例。
1. 指定要吊销的策略ID。
1. 使用刚刚创建的策略ID `String`创建`PolicyRevocationEntry`对象，并将其传递到`PolicyUpdateListFactory.addRevocationEntry()`以将其添加到策略更新列表。 通过调用`PolicyUpdateListFactory.generatePolicyUpdateList()`生成新策略更新列表。 同样，可以使用`PolicyUpdateEntry`将更新的策略添加到列表。
1. 如果策略更新列表已存在，则可以通过调用`PolicyUpdateList.getBytes()`对其进行序列化以进行加载。 要加载列表，请调用`PolicyUpdateListFactory.loadPolicyUpdateList()`并传入序列化列表。
1. 通过调用`PolicyUpdateList.verifySignature()`验证签名是否有效，且列表已由正确的许可证服务器证书签名。
1. 要检查是否已吊销某条目，请将策略ID `String`传递到`PolicyUpdateList.isRevoked()`。 或者，列表可以传递到`HandlerConfiguration`中，并在颁发许可证时强制执行。

要向现有`PolicyUpdateList`添加其他条目，请加载现有策略更新列表。 新建一个`PolicyUpdateListFactory`实例。 调用P `olicyUpdateListFactory.addEntries`将旧列表中的所有条目添加到新列表。 调用`PolicyUpdateListFactory.addRevocationEntry`或`addUpdatedEntry`将任何新的吊销或更新条目添加到PolicyUpdateList。

有关演示如何创建策略更新列表、加载现有策略更新列表以及检查策略是否已吊销的示例代码，请参阅Reference Implementation命令行工具“samples”目录中的`com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList`。
