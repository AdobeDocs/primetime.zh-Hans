---
description: 如果您使用Adobe PrimetimeDRM专业版，您可以预生成许可证并将许可证嵌入到内容中。 此功能可以与“增强的许可证链”结合使用，这样，Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。
seo-description: 如果您使用Adobe PrimetimeDRM专业版，您可以预生成许可证并将许可证嵌入到内容中。 此功能可以与“增强的许可证链”结合使用，这样，Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。
seo-title: 预生成许可证
title: 预生成许可证
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# 预生成许可证{#pre-generating-licenses}

如果您使用Adobe PrimetimeDRM专业版，您可以预生成许可证并将许可证嵌入到内容中。 此功能可以与“增强的许可证链”结合使用，这样，Leaf许可证就预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实现一个工作流，其中设备预注册到服务器，服务器预生成绑定到该设备的许可证，并且客户端从简单的HTTP Web服务器检索其许可证。

如果要预生成许可证，必须使用`com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()`获取`LicenseFactory`的实例。 必须指定许可证服务器凭据才能对此工厂生成的许可证进行签名。 此类支持生成无许可证链接的Leaf许可证，以及使用[增强许可证链接](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)生成Leaf和Root许可证。

生成Leaf许可证时，必须指定应用`initContentInfo()`的内容元数据。 如果元数据包括多个DRM策略，或者如果要使用未包含在元数据中的DRM策略，则必须使用`setSelectedPolicy()`指定DRM策略以生成许可证。 如果使用DRM策略更新列表跟踪DRM策略的更新，则在使用`setPolicyUpdateList()`初始化元数据之前，可以为许可证工厂提供DRM策略更新列表。

在生成根许可证时，必须指定上述内容元数据。 或者，您也可以通过应用DRM策略(`setSelectedPolicy()`)和许可证服务器URL(`setLicenseServerURL()`)而不是元数据来生成根许可证。

>[!NOTE]
>
>即使没有客户端可以请求许可证的Adobe PrimetimeDRM许可证服务器，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果DRM策略使用增强的许可证链，则必须指定许可证服务器凭据才能在DRM策略(`setRootKeyRetrievalInfo()`)中解密根加密密钥。

如果DRM策略需要域绑定许可证，则必须使用`setDomainCAs()`指定许可证服务器从中接受域令牌的域发行者。 必须提供一个或多个域CA证书以验证许可收件人。

如果DRM策略要求对iOS设备进行远程密钥投放，则必须通过应用`setKeyServerCertificate()`来提供密钥服务器证书，除非生成链式叶。

如果要生成许可证，必须调用`generateLicense()`并指定许可证类型（Leaf或Root）和一个或多个收件人证书。 收件人证书表示计算机证书或域证书，具体取决于DRM策略中指定的要求。 如果生成链式叶，则不需要收件人。 在生成许可证后，您可以覆盖在DRM策略中指定的使用规则。 最后，您需要调用`signLicense()`对许可证进行签名并获取`PreGeneratedLicense`的实例。 现在可以保存许可证(使用`getBytes()`检索序列化许可证或嵌入到加密内容中。

请参阅[嵌入许可证](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md)。

有关如何演示预生成的许可证的示例代码，请参阅参考实施命令行工具“samples”目录中的`com.adobe.flashaccess.samples.licensegen.GenerateLicense`。
