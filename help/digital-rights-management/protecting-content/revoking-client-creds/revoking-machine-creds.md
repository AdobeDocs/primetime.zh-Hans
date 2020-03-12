---
seo-title: 撤销计算机凭据
title: 撤销计算机凭据
uuid: 3647c843-5f1a-457e-949d-10a6278b1c29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 撤销计算机凭据 {#revoking-machine-credentials}

Adobe维护一个CRL，用于撤销已知会泄露的计算机凭据。 此CRL由SDK自动实施。 如果您不希望您的许可证服务器向其他计算机颁发许可证，则可以创建计算机撤销列表，并添加要排除的计算机令牌的颁发者名称和序列号（用于检索计算机证书的颁发者名称和序列号）。 `MachineToken.getMachineTokenId()`

撤销计算机凭据涉及对象的使 `RevocationListFactory` 用。 要创建撤销列表，请加载现有的撤销列表，并使用Java API检查计算机令牌是否已被撤销，请执行以下步骤：

1. 设置开发环境，并将“设置开发环境”中提 [及的所有JAR文件包含在项目中](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) 。
1. 创建一 `ServerCredentialFactory` 个实例以加载签名所需的凭据。 许可证服务器凭据用于签署吊销列表。
1. 创建实 `RevocationListFactory` 例。
1. 使用对象指定要撤销的计算机令牌的发行商和序列 `IssuerAndSerialNumber` 号。 所有Adobe Primetime DRM请求都包含机器令牌。
1. 使用刚 `RevocationList` 创建的对象创 `IssuerAndSerialNumber` 建一个对象，并通过将其传入吊销列表将其添加到撤销列表 `RevocationListFactory.addRevocationEntry()`。 通过调用生成新的撤销列表 `RevocationListFactory.generateRevocationList()`。

1. 要保存撤销列表，您可以通过调用将其序列化 `RevocationList.getBytes()`。 要加载列表，请调 `RevocationListFactory.loadRevocationList()` 用并传入序列化列表。

1. 通过调用验证签名是否有效以及列表是否已由正确的许可证服务器签名 `RevocationList.verifySignature()`。
1. 要检查某条目是否被撤销，请将该对 `IssuerAndSerialNumber` 象传递到 `RevocationList.isRevoked()`。 吊销列表也可能会被传递到SDK `HandlerConfiguration` 以强制所有身份验证和许可证请求的吊销列表。

要向现有条目添加其他条目， `RevocationList`请加载现有的撤销列表。 创建新 `RevocationListFactory` 实例，并确保增加CRL编号。 调 `RevocationListFactioryEntries.addRevocationEntries` 用以将旧列表中的所有条目添加到新列表。 调 `RevocationListFactory.addRevocationEntry` 用以向RevocationList添加任何新的撤销条目。

有关如何创建撤销列表、加载现有撤销列表以及检查计算机令牌是否已被撤销的示例代码，请参 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 阅Reference Implementation Command Line Tools目 [!DNL samples] 录。
