---
description: 如果您使用Adobe Primetime DRM Professional，则可以在内容中预生成许可证并嵌入许可证。 此功能可以与增强许可证链结合使用，这样Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。
title: 预生成许可证
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# 预生成许可证{#pre-generating-licenses}

如果您使用Adobe Primetime DRM Professional，则可以在内容中预生成许可证并嵌入许可证。 此功能可以与增强许可证链结合使用，这样Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。

如果要预生成许可证，则必须使用`com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()`获取`LicenseFactory`的实例。 必须指定License Server凭据才能对此工厂生成的许可证进行签名。 此类支持生成无许可证链接的Leaf许可证，以及使用[增强许可证链接](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)的Leaf和Root许可证。

生成Leaf许可证时，必须指定应用`initContentInfo()`的内容元数据。 如果元数据包括多个DRM策略，或者如果要使用尚未包含在元数据中的DRM策略，则必须使用`setSelectedPolicy()`指定DRM策略以生成许可证。 如果您使用DRM策略更新列表来跟踪DRM策略的更新，则在使用`setPolicyUpdateList()`初始化元数据之前，可以向许可证工厂提供DRM策略更新列表。

生成根许可证时，必须指定上述内容元数据。 或者，您也可以通过应用DRM策略(`setSelectedPolicy()`)和许可证服务器URL(`setLicenseServerURL()`)（而非元数据）来生成根许可证。

>[!NOTE]
>
>即使没有Adobe Primetime DRM许可证服务器，客户端也可以从中请求许可证，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果DRM策略使用“增强的许可证链”，则必须指定许可证服务器凭据才能在DRM策略(`setRootKeyRetrievalInfo()`)中解密根加密密钥。

如果DRM策略需要域绑定的许可证，则必须使用`setDomainCAs()`指定许可证服务器从中接受域令牌的域发行商。 必须提供一个或多个域CA证书以验证许可收件人。

如果DRM策略要求对iOS设备进行远程密钥投放，则必须通过应用`setKeyServerCertificate()`来提供密钥服务器证书，除非生成链式Leaf。

如果要生成许可证，必须调用`generateLicense()`并指定许可证类型（Leaf或Root）和一个或多个收件人证书。 收件人证书表示计算机证书或域证书，具体取决于在DRM策略中指定的要求。 如果生成链式叶，则不需要收件人。 生成许可证后，您可以覆盖在DRM策略中指定的使用规则。 最后，您需要调用`signLicense()`对许可证进行签名并获取`PreGeneratedLicense`的实例。 现在可以保存许可证（使用`getBytes()`检索序列化许可证或嵌入加密内容中）。

请参阅[嵌入许可证](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md)。

请参见参考实施命令行工具“samples”目录中的`com.adobe.flashaccess.samples.licensegen.GenerateLicense`，了解有关如何演示预生成许可证的示例代码。
