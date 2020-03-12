---
description: 如果您使用Adobe Primetime DRM Professional，则可以预生成许可证并将许可证嵌入到内容中。 此功能可以与增强的许可证链接结合使用，这样，Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。
seo-description: 如果您使用Adobe Primetime DRM Professional，则可以预生成许可证并将许可证嵌入到内容中。 此功能可以与增强的许可证链接结合使用，这样，Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。
seo-title: 预生成许可证
title: 预生成许可证
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 预生成许可证 {#pre-generating-licenses}

如果您使用Adobe Primetime DRM Professional，则可以预生成许可证并将许可证嵌入到内容中。 此功能可以与增强的许可证链接结合使用，这样，Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。

如果要预生成许可证，则必须使 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 用获得实例 `LicenseFactory`。 您必须指定许可证服务器凭据才能对此工厂生成的许可证进行签名。 此类支持生成不带许可证链接的Leaf许可证，以及具有增强许可证链接的Leaf和 [Root许可证](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)。

在生成Leaf许可证时，必须指定适用的内容元数据 `initContentInfo()`。 如果元数据包括多个DRM策略，或者如果要使用元数据中未包含的DRM策略，则必须使用指定 `setSelectedPolicy()` DRM策略来生成许可证。 如果使用DRM策略更新列表跟踪DRM策略的更新，则可以在初始化元数据之前，将DRM策略更新列表提供到许可证工厂 `setPolicyUpdateList()`。

在生成根许可证时，必须指定上述内容元数据。 或者，您也可以通过应用DRM策略( `setSelectedPolicy()`)和许可证服务器URL()而不是元数据来生成根许 `setLicenseServerURL()`可证。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>即使没有客户端可以从中请求许可的Adobe Primetime DRM许可证服务器，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果DRM策略使用增强的许可证链接，则必须指定许可证服务器凭据以解密DRM策略( `setRootKeyRetrievalInfo()`)中的根加密密钥。

如果DRM策略需要域绑定许可证，则您必须使 `setDomainCAs()` 用指定许可证服务器从中接受域令牌的域发行商。 必须提供一个或多个域CA证书以验证许可证收件人。

如果DRM策略要求为iOS设备提供远程密钥交付，则必须通过应用提供密钥服务器证书，除非生 `setKeyServerCertificate()` 成链式叶。

如果要生成许可证，则必须调用并指 `generateLicense()` 定许可证类型（Leaf或Root）以及一个或多个收件人证书。 接收方证书表示计算机证书或域证书，具体取决于在DRM策略中指定的要求。 如果生成链式Leaf，则不需要收件人。 在生成许可证后，您可以覆盖在DRM策略中指定的使用规则。 最后，您需要调用 `signLicense()` 以对许可证进行签名并获取实例 `PreGeneratedLicense`。 现在可以保存许可证(用于 `getBytes()` 检索序列化许可证或嵌入到加密内容中)。

请参阅 [嵌入许可证](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md)。

请参 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 阅参考实施命令行工具“示例”目录，了解有关如何展示预生成许可证的示例代码。
