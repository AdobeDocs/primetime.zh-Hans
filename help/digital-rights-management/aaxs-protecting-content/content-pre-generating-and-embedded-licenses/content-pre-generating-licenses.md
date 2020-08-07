---
seo-title: 预生成许可证
title: 预生成许可证
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 预生成许可证{#pre-generating-licenses}

要预生成许可证，请 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 使用获取实例 `LicenseFactory`。 必须指定许可证服务器凭据才能对此工厂生成的许可证进行签名。 此类支持生成无许可证链接的Leaf许可证，以及增强许可证链接的Leaf和 [Root许可证](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md)。

生成Leaf许可证时，必须使用指定内容元数据 `initContentInfo()`。 如果元数据包括多个策略，或者如果要使用元数据中未包含的策略，则 `setSelectedPolicy()` 使用指定用于生成许可证的策略。 如果使用策略更新列表跟踪策略的更新，则可以在使用初始化元数据之前，向许可证工厂提供策略更新列表 `setPolicyUpdateList()`。

在生成根许可证时，可以按如上所述指定内容元数据。 或者，可以使用策略()和许可证服 `setSelectedPolicy()`务器URL()(而 `setLicenseServerURL()`不是元数据)生成根许可证。

>[!NOTE]
>
>即使没有Adobe访问许可证服务器，客户端也可以从中请求许可证，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果策略使用增强的许可证链，则必须指定许可证服务器凭据才能解密策略()中的根加密 `setRootKeyRetrievalInfo()`密钥。

如果策略需要域绑定许可证，请 `setDomainCAs()` 使用指定许可证服务器接受域令牌的域发行者。 必须提供一个或多个域CA证书才能验证许可收件人。

如果策略要求对iOS设备进行远程密钥投放，则必须使用提供密钥服务器证书， `setKeyServerCertificate()`除非生成链式Leaf。

要生成许可证，请调 `generateLicense()` 用并指定许可证类型（Leaf或Root）以及一个或多个收件人证书。 收件人证书将是计算机证书或域证书，具体取决于策略中指定的要求。 如果生成链式叶，则不需要收件人。 在生成许可证后，可以覆盖策略中指定的使用规则。 最后，调 `signLicense()` 用对许可证进行签名并获取实例 `PreGeneratedLicense`。 许可证现在可保存到文件(用于检 `getBytes()` 索序列化许可证)或嵌入到加密内容中。 请参阅嵌 [入许可证](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md)。

有关演示预生成许可证的示例代码， `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 请参阅参考实施命令行工具“示例”目录。
