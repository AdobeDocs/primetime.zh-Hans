---
seo-title: 撤销计算机凭据
title: 撤销计算机凭据
uuid: 16119ff9-8147-4fe0-9744-a705d94a9400
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# 撤销计算机凭据{#revoking-machine-credentials}

Adobe保留CRL以撤销已知会泄露的计算机凭据。 此CRL由SDK自动强制执行。 如果您不希望您的许可证服务器向其颁发许可证的其他计算机，您可以创建计算机吊销列表并添加要排除的计算机令牌的颁发者名称和序列号（使用`MachineToken.getMachineTokenId()`检索计算机证书的颁发者名称和序列号）。

撤销计算机凭据涉及`RevocationListFactory`对象的使用。 要创建吊销列表，加载现有吊销列表，并使用Java API检查计算机令牌是否已吊销，请执行以下步骤：

1. 设置开发环境并包含[设置项目中的开发环境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)中提及的所有JAR文件。
1. 创建`ServerCredentialFactory`实例以加载签名所需的凭据。 许可证服务器凭据用于签署吊销列表。
1. 创建`RevocationListFactory`实例。
1. 使用`IssuerAndSerialNumber`对象指定要撤销的计算机令牌的颁发者和序列号。 所有Adobe访问请求都包含计算机令牌。
1. 使用您刚刚创建的`IssuerAndSerialNumber`对象创建`RevocationList`对象，并通过将其传递到`RevocationListFactory.addRevocationEntry()`将其添加到吊销列表。 通过调用`RevocationListFactory.generateRevocationList()`生成新的吊销列表。
1. 要保存吊销列表，可通过调用`RevocationList.getBytes()`将其序列化。 要加载列表，请调用`RevocationListFactory.loadRevocationList()`并传入序列化列表。
1. 通过调用`RevocationList.verifySignature()`验证签名是否有效以及列表是否已由正确的许可证服务器进行签名。
1. 要检查条目是否被吊销，请将`IssuerAndSerialNumber`对象传递到`RevocationList.isRevoked()`。 吊销列表也可以传递到`HandlerConfiguration`，以使SDK对所有身份验证和许可证请求强制执行吊销列表。

要向现有`RevocationList`添加其他条目，请加载现有吊销列表。 新建一个`RevocationListFactory`实例，并确保增加CRL编号。 调用`RevocationListFactioryEntries.addRevocationEntries`将旧列表中的所有条目添加到新列表。 调用`RevocationListFactory.addRevocationEntry`将任何新的吊销条目添加到RevocationList。

有关演示如何创建撤销列表、加载现有撤销列表以及检查计算机令牌是否已被撤销的示例代码，请参见Reference Implementation Command Line Tools &quot;samples&quot;目录中的`com.adobe.flashaccess.samples.revocation.CreateRevocationList`。
