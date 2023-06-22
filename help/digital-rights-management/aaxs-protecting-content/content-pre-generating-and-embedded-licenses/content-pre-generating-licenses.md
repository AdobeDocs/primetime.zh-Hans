---
title: 预生成许可证
description: 预生成许可证
copied-description: true
exl-id: 2be8674c-736f-4ed3-b952-f661bf3ff48f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 预生成许可证{#pre-generating-licenses}

要预生成许可证，请使用 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 获取实例 `LicenseFactory`. 必须指定许可证服务器凭据才能对此工厂生成的许可证进行签名。 此类支持生成不带许可证链接的叶许可证，以及带许可证的叶和根许可证 [增强型许可证链接](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

在生成Leaf许可证时，必须使用指定内容元数据 `initContentInfo()`. 如果元数据包含多个策略，或者如果您希望使用元数据中没有的策略，请使用 `setSelectedPolicy()` 指定要用于生成许可证的策略。 如果使用策略更新列表跟踪策略更新，则可以在初始化元数据之前向许可证工厂提供策略更新列表 `setPolicyUpdateList()`.

在生成Root许可证时，可以按如上所述方式指定内容元数据。 或者，可以使用策略( `setSelectedPolicy()`)和许可证服务器URL ( `setLicenseServerURL()`)而不是元数据。

>[!NOTE]
>
>即使没有Adobe访问许可证服务器，客户端也可以从中请求许可证，也需要License Server URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果策略使用增强型许可证链接，则必须指定许可证服务器凭据才能解密策略中的根加密密钥( `setRootKeyRetrievalInfo()`)。

如果策略需要绑定域的许可证，请使用 `setDomainCAs()` 指定许可证服务器将从中接受域令牌的域颁发者。 必须提供一个或多个域CA证书才能验证许可证收件人。

如果策略要求为iOS设备远程交付密钥，则必须使用以下方式提供密钥服务器证书 `setKeyServerCertificate()`，除非生成链接的Leaf。

要生成许可证，请调用 `generateLicense()` 和指定许可证类型（叶或根）以及一个或多个收件人证书。 收件人证书可以是计算机证书或域证书，具体取决于策略中指定的要求。 如果要生成链接叶，则不需要收件人。 生成许可证后，可以覆盖策略中指定的使用规则。 最后，调用 `signLicense()` 签署许可证并获取 `PreGeneratedLicense`. 许可证现在可以保存到文件(使用 `getBytes()` 以检索序列化许可证)或嵌入到加密内容中。 参见， [嵌入许可证](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

有关演示预生成许可证的示例代码，请参阅 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 在参考实施命令行工具“samples”目录中。
