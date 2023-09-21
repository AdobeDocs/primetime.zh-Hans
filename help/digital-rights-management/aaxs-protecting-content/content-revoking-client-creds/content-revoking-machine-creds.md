---
title: 正在撤销计算机凭据
description: 正在撤销计算机凭据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# 正在撤销计算机凭据{#revoking-machine-credentials}

Adobe维护一个CRL，用于撤销已知受到危害的计算机凭据。 此CRL由SDK自动强制执行。 如果存在不希望许可证服务器向其颁发许可证的其他计算机，则可以创建计算机吊销列表，并添加要排除的计算机令牌的颁发者名称和序列号(使用 `MachineToken.getMachineTokenId()` 以检索计算机证书的颁发者名称和序列号)。

撤销计算机凭据涉及使用 `RevocationListFactory` 对象。 要创建吊销列表，请加载现有的吊销列表，并检查计算机令牌是否已使用Java API吊销，请执行以下步骤：

1. 设置开发环境，并包含中提到的所有JAR文件 [设置开发环境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 在您的项目中。
1. 创建 `ServerCredentialFactory` 用于加载签名所需的凭据的实例。 许可证服务器凭据用于对吊销列表进行签名。
1. 创建 `RevocationListFactory` 实例。
1. 使用指定要撤消的计算机令牌的颁发者和序列号 `IssuerAndSerialNumber` 对象。 所有Adobe访问请求都包含一个计算机令牌。
1. 创建 `RevocationList` 对象使用 `IssuerAndSerialNumber` 您刚刚创建的对象，并通过将其传递到以将其添加到吊销列表 `RevocationListFactory.addRevocationEntry()`. 通过调用生成新的吊销列表 `RevocationListFactory.generateRevocationList()`.
1. 要保存吊销列表，可以通过调用 `RevocationList.getBytes()`. 要加载列表，请调用 `RevocationListFactory.loadRevocationList()` 并在序列化列表中传递。
1. 通过调用，验证签名是否有效以及列表是否由正确的许可证服务器签名 `RevocationList.verifySignature()`.
1. 要检查某个条目是否被撤销，请传递 `IssuerAndSerialNumber` 对象移入 `RevocationList.isRevoked()`. 吊销列表也可以传递到 `HandlerConfiguration` 以使SDK强制所有身份验证和许可证请求的吊销列表。

向现有条目添加附加条目 `RevocationList`，加载现有的吊销列表。 新建 `RevocationListFactory` 实例中，并确保递增CRL编号。 调用 `RevocationListFactioryEntries.addRevocationEntries` 将旧列表中的所有条目添加到新列表中。 调用 `RevocationListFactory.addRevocationEntry` 向RevocationList中添加任何新的吊销条目。

有关演示如何创建吊销列表、加载现有吊销列表以及检查计算机令牌是否已被吊销的示例代码，请参阅 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 在参考实施命令行工具“samples”目录中。
