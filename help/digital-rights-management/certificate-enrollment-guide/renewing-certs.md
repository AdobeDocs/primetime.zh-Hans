---
title: 续订证书
description: 续订证书
copied-description: true
exl-id: db130ca5-4e26-447f-b2f4-4eee0838fd56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 续订证书{#renew-certificates}

您应了解以下基于您的Adobe Primetime DRM SDK配置的证书续订限制：

* Primetime DRM生产SDK

   当您购买支持合同时，Adobe会为Primetime DRM生产SDK提供初始的免费证书集。 如果您没有支持合同，则可以购买一组有效期为两年的续订证书。
* Primetime DRM评估SDK

   此SDK的证书集的有效期为一年，无法续订。
* Primetime DRM试用版SDK

   Primetime DRM试用版SDK的有效期为三个月，而Adobe提供一组免费的续订证书。

## 实施新证书并对现有内容使用旧证书 {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

在Primetime DRM中，您可以允许许可证服务器为使用以前的（甚至过期的）打包程序证书打包的内容颁发许可证。 要将您的服务器配置为接受来自先前打包内容的许可证请求，请将旧证书提供给您的服务器并更新服务器的配置文件，以便服务器知道在何处查找旧证书。 有关更多信息，请参阅 *处理Adobe颁发的证书过期时的证书更新* 在 *使用Adobe Primetime DRM SDK保护内容*.

如果您的服务器应用程序基于Primetime DRM参考实施，则无需更新服务器端程序。 在 `flashaccess-refimpl.properties` 文件，您可在其中指定其他传输和许可证服务器证书的字段。 如果您只有一个证书，则无需填充这些属性。 如果您拥有过期的证书，并且希望在发出许可证响应时使用这些证书，则必须将这些证书提供给配置文件并重新启动服务器。

要指定旧证书，请使用以下属性：

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
