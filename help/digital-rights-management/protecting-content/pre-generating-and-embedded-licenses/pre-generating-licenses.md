---
description: 如果您使用Adobe Primetime DRM Professional，则可以在内容中预生成许可证和嵌入许可证。 此功能可与增强型许可证链接相结合，以便Leaf许可证被预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实施一个工作流，其中设备向服务器预注册，服务器预生成绑定到该设备的许可证，客户端从简单的HTTP Web服务器检索其许可证。
title: 预生成许可证
exl-id: 6ced7dde-b4bb-470d-bdae-3042f5577b67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 预生成许可证 {#pre-generating-licenses}

如果您使用Adobe Primetime DRM Professional，则可以在内容中预生成许可证和嵌入许可证。 此功能可与增强型许可证链接相结合，以便Leaf许可证被预生成并嵌入到内容中，并且客户端可以从许可证服务器请求根许可证（绑定到计算机或域）。 或者，客户端应用程序可以实施一个工作流，其中设备向服务器预注册，服务器预生成绑定到该设备的许可证，客户端从简单的HTTP Web服务器检索其许可证。

如果要预生成许可证，则必须使用 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 获取实例 `LicenseFactory`. 必须指定许可证服务器凭据以签署由此工厂生成的许可证。 此类支持生成不带许可证链接的叶许可证，以及带许可证的叶和根许可证 [增强型许可证链接](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

在生成Leaf许可证时，必须指定适用的内容元数据 `initContentInfo()`. 如果元数据包含多个DRM策略，或者如果您要使用元数据中未包含的DRM策略，则必须使用 `setSelectedPolicy()` 指定要生成许可证的DRM策略。 如果使用DRM策略更新列表来跟踪DRM策略的更新，则可以在初始化元数据之前将DRM策略更新列表提供给许可证工厂 `setPolicyUpdateList()`.

在生成Root许可证时，必须指定内容元数据，如上所述。 或者，您可以通过应用DRM策略( `setSelectedPolicy()`)和许可证服务器URL ( `setLicenseServerURL()`)而不是元数据。

>[!NOTE]
>
>即使没有客户端可以从中请求许可证的Adobe Primetime DRM许可证服务器，也需要许可证服务器URL。 在这种情况下，许可证服务器URL应指定标识许可证颁发者的URL。

如果DRM策略使用增强型许可证链接，则必须指定许可证服务器凭据来解密DRM策略中的根加密密钥( `setRootKeyRetrievalInfo()`)。

如果DRM策略需要域绑定的许可证，则必须使用 `setDomainCAs()` 以指定许可证服务器从中接受域令牌的域颁发者。 必须提供一个或多个域CA证书来验证许可证收件人。

如果DRM策略要求iOS设备的远程密钥交付，则必须通过应用提供密钥服务器证书 `setKeyServerCertificate()` 除非正在生成链接的Leaf。

如果要生成许可证，则必须调用 `generateLicense()` 和指定许可证类型（叶或根）以及一个或多个收件人证书。 收件人证书表示计算机证书或域证书，具体取决于DRM策略中指定的要求。 如果生成链接叶，则不需要收件人。 生成许可证后，您可以覆盖DRM策略中指定的使用规则。 最后，您需要调用 `signLicense()` 签署许可证并获取 `PreGeneratedLicense`. 现在可以保存许可证(使用 `getBytes()` 检索序列化许可证或嵌入加密内容中的许可证。

参见 [嵌入许可证](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

参见 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 在参考实施命令行工具“示例”目录中，查看有关如何演示预生成许可证的示例代码。
