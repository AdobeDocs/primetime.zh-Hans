---
title: 使用DRM策略更新列表
description: 使用DRM策略更新列表
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# DRM策略更新列表{#drm-policy-update-lists}

如果在打包任何内容后更新DRM策略中的使用规则，则许可证服务器需要具有最新版本，然后才能发放使用已更新DRM策略的许可证。 实现这一点的一种方法是通过DRM策略更新列表。

DRM策略更新列表由包含更新或已吊销DRM策略列表的文件表示。 每次更新DRM策略时，您都需要生成新的DRM策略更新列表，并定期将列表推送到所有许可证服务器。

## 使用DRM策略更新列表{#working-with-drm-policy-update-lists}

对于无权访问存储有关DRM策略的信息的数据库的许可证服务器，您可能希望使用DRM策略更新列表来通知许可证服务器任何已更新的DRM策略。 DRM策略更新列表可以包括已吊销的DRM策略的更新版本或DRM策略ID的列表。 如果`HandlerConfiguration`中包含策略更新列表，则SDK在发布许可证时强制执行此列表。

如果内容所有者或分发者希望根据特定DRM策略停止颁发许可证，您还可以撤销任何DRM策略。 DRM策略更新列表可用于在SDK中强制DRM策略吊销。 您还可以应用DRM策略更新列表，以向SDK提供更新的DRM策略的列表。

>[!NOTE]
>
>在您撤销DRM策略时，不会自动撤销已颁发的所有许可证。 它只会阻止根据该DRM政策发放其他许可证。

## 更新策略更新列表{#update-policy-update-lists}

使用DRM策略更新列表涉及使用`PolicyUpdateListFactory`对象。 如果要创建DRM策略更新列表，您需要加载现有的DRM策略更新列表，然后使用Java API检查DRM策略是否已更新或吊销。

要使用DRM策略更新列表:

1. 设置开发环境并包括在项目中设置开发环境时包含的所有JAR文件。
1. 创建一个`ServerCredentialFactory`实例以加载签名所需的凭据。
1. 使用您创建的`ServerCredential`创建`PolicyUpdateListFactory`实例。
1. 指定要撤销的DRM策略ID。
1. 使用您刚刚创建的DRM策略ID `String`创建`PolicyRevocationEntry`对象，然后将其传递到`PolicyUpdateListFactory.addRevocationEntry()`，将其添加到DRM策略更新列表。
1. 通过调用`PolicyUpdateListFactory.generatePolicyUpdateList()`生成新的DRM策略更新列表。

   同样，您也可以使用`PolicyUpdateEntry`将DRM策略更新到列表。
1. 如果DRM策略更新列表已存在，则可以通过调用`PolicyUpdateList.getBytes()`对其进行序列化以加载。

   要加载列表，请调用`PolicyUpdateListFactory.loadPolicyUpdateList()`并在序列化列表中传递它。
1. 通过调用`PolicyUpdateList.verifySignature()`验证签名是否有效以及列表是否已由正确的许可证服务器证书签名。
1. 将DRM策略ID `String`传递到`PolicyUpdateList.isRevoked()`以验证某个条目是否已吊销。

   或者，您也可以将列表传递到`HandlerConfiguration`，在此处，每当发放许可证时，都会强制执行该操作。
如果要向现有`PolicyUpdateList`添加更多条目，则需要加载现有DRM策略更新列表。 因此，您需要创建新的DRM `PolicyUpdateListFactory`实例。 调用`PolicyUpdateListFactory.addEntries`将旧列表中的所有条目添加到新列表。 调用`PolicyUpdateListFactory.addRevocationEntry`或`addUpdatedEntry`将任何新的吊销或更新条目添加到DRM PolicyUpdateList。

有关演示如何创建DRM策略更新列表的示例代码，请参阅&#x200B;*参考实现命令行工具* [!DNL samples]目录中的`com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList`。
