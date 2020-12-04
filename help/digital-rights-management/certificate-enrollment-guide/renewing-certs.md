---
seo-title: 续订证书
title: 续订证书
uuid: 12a560b0-966b-424e-bfe5-22e9c10d8667
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# 续订证书{#renew-certificates}

您应注意以下基于您的Adobe PrimetimeDRM SDK配置的证书续订限制：

* Primetime DRM Production SDK

   Adobe在您购买支持合同时为Primetime DRM Production SDK提供初始的免费证书集。 如果您没有支持合同，则可以购买一组有效期为两年的续订证书。
* Primetime DRM评估SDK

   此SDK的证书集的有效期为一年，无法续订。
* Primetime DRM试用版SDK

   Primetime DRM试用版SDK的有效期为三个月，Adobe提供一套免费的续订证书。

## 为现有内容{#section_345C92D1C9794B0BBB9A9B0702EC95FF}实施新证书和使用旧证书

在Primetime DRM中，您可以允许许可证服务器为与先前（甚至已过期）包装程序证书一起打包的内容颁发许可证。 要将服务器配置为接受来自先前打包内容的许可证请求，请向服务器提供您的旧证书并更新服务器的配置文件，以便服务器知道在何处找到旧证书。 有关详细信息，请参阅&#x200B;*使用Adobe PrimetimeDRM SDK保护内容*&#x200B;中的&#x200B;*当Adobe颁发的证书过期时处理证书更新。*

如果您的服务器应用程序基于Primetime DRM参考实施，则无需更新服务器端项目。 在`flashaccess-refimpl.properties`文件中，有一些字段可以指定其他传输和许可证服务器证书。 如果您只有一个证书，则不必填充这些属性。 如果您已过期的证书，并且希望在您发出许可证响应时使用这些证书，则必须向配置文件提供这些证书并重新启动服务器。

要指定旧证书，请使用以下属性：

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

