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

要预生成许可证，请使用`com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()`获取`LicenseFactory`的实例。 必须指定许可证服务器凭据才能对此工厂生成的许可证进行签名。 此类支持生成无许可证链接的Leaf许可证，以及使用[增强许可证链接](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md)生成Leaf和Root许可证。

生成Leaf许可证时，必须使用`initContentInfo()`指定内容元数据。 如果元数据包含多个策略，或者如果要使用不在元数据中的策略，请使用`setSelectedPolicy()`指定用于生成许可证的策略。 如果使用策略更新列表跟踪策略更新，则可在使用`setPolicyUpdateList()`初始化元数据之前向许可证工厂提供策略更新列表。

在生成根许可证时，可以按如上所述指定内容元数据。 或者，可以使用策略(`setSelectedPolicy()`)和许可证服务器URL(`setLicenseServerURL()`)生成根许可证，而不是元数据。

>[!NOTE]
>
>即使没有Adobe访问许可证服务器，客户端也可以从中请求许可证，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果策略使用“增强的许可证链”，则必须指定许可证服务器凭据才能解密策略中的根加密密钥(`setRootKeyRetrievalInfo()`)。

如果策略需要域绑定许可证，请使用`setDomainCAs()`指定许可证服务器将接受域令牌的域发行方。 必须提供一个或多个域CA证书才能验证许可收件人。

如果策略要求对iOS设备进行远程密钥投放，则必须使用`setKeyServerCertificate()`提供密钥服务器证书，除非生成链式叶。

要生成许可证，请调用`generateLicense()`并指定许可证类型（Leaf或Root）和一个或多个收件人证书。 收件人证书将是计算机证书或域证书，具体取决于策略中指定的要求。 如果生成链式叶，则不需要收件人。 在生成许可证后，可以覆盖策略中指定的使用规则。 最后，调用`signLicense()`对许可证进行签名并获取`PreGeneratedLicense`的实例。 许可证现在可保存到文件（使用`getBytes()`检索序列化许可证）或嵌入到加密内容中。 请参阅[嵌入许可证](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md)。

有关演示预生成许可证的示例代码，请参阅参考实施命令行工具“samples”目录中的`com.adobe.flashaccess.samples.licensegen.GenerateLicense`。
