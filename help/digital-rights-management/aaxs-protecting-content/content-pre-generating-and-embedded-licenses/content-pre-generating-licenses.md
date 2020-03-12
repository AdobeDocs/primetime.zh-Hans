---
seo-title: 预生成许可证
title: 预生成许可证
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 预生成许可证{#pre-generating-licenses}

要预生成许可证，请 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 使用获取实例 `LicenseFactory`。 必须指定许可证服务器凭据才能对此工厂生成的许可证进行签名。 此类支持生成不带许可证链接的Leaf许可证，以及具有增强许可证链接的Leaf和 [Root许可证](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md)。

在生成Leaf许可证时，必须使用指定内容元数据 `initContentInfo()`。 如果元数据包括多个策略，或者如果要使用不在元数据中的策略，请使用指定用于生 `setSelectedPolicy()` 成许可证的策略。 如果您使用策略更新列表跟踪策略的更新，则可以在使用初始化元数据之前将策略更新列表提供到许可证工厂 `setPolicyUpdateList()`。

在生成根许可证时，可以按上述说明指定内容元数据。 或者，可以使用策略( `setSelectedPolicy()`)和许可证服务器URL()而不是元数据生成根 `setLicenseServerURL()`许可证。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>即使没有客户端可以从中请求许可证的Adobe Access许可证服务器，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果策略使用增强的许可证链，则必须指定许可证服务器凭据才能解密策略( `setRootKeyRetrievalInfo()`)中的根加密密钥。

如果策略需要域绑定许可证，请使 `setDomainCAs()` 用指定许可证服务器将从中接受域令牌的域发行者。 必须提供一个或多个域CA证书才能验证许可证收件人。

如果策略要求为iOS设备提供远程密钥交付，则必须使用提供密钥服务器证书 `setKeyServerCertificate()`，除非生成链式Leaf。

要生成许可证，请调用并 `generateLicense()` 指定许可证类型（Leaf或Root）和一个或多个收件人证书。 收件人证书将是计算机证书或域证书，具体取决于策略中指定的要求。 如果生成链式Leaf，则不需要收件人。 在生成许可证后，可以覆盖在策略中指定的使用规则。 最后，调用 `signLicense()` 以对许可证进行签名并获取实例 `PreGeneratedLicense`。 许可证现在可保存到文件(用于检索序列 `getBytes()` 化许可证)或嵌入到加密内容中。 请参阅嵌入 [许可证](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md)。

有关演示预生成许可证的示例代码，请参 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 阅参考实施命令行工具“示例”目录。
