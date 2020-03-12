---
description: Multi CDN允许设置一个或多个CDN位置以提供转码广告。
seo-description: Multi CDN允许设置一个或多个CDN位置以提供转码广告。
seo-title: 多CDN支持
title: 多CDN支持
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# 多CDN支持 {#multi-cdn-support}

Multi CDN允许设置一个或多个CDN位置以提供转码广告。

默认情况下，所有转码的资源都托管在Adobe拥有的Akamai CDN上。 但是，您可以选择您自己的零个或更多其他CDN位置，CRS将在该位置托管转码的资产。 因此，在这种情况下，可以从同一CDN提供转码的资源和内容。

当清单服务器查找转码请求时，它使用包含许多查询参数的引导URL。 如果您设置了多CDN环境，引导URL也需要包含该参数。清单服务器使用此参数来标识从中获取转码版本的广告的CDN服务器。 `ptcdn`

还提供以下Primetime解决方案的多CDN支持：

1. 适用于Android的TVSDK
1. 桌面HLS的TVSDK
1. iOS版TVSDK

## 启用CDN支持 {#section_1BA344F2300B49F291865A7461EDFEAE}

默认情况下，CRS对于所有客户都处于禁用状态

联系您的Adobe技术客户经理，将您的CRS帐户配置为使用其他CDN来托管转码广告资产。您需要提供CRS将转码广告资产上传到CDN所需的以下信息

1. CDN URL
1. 身份验证详细信息
1. 输出URL格式

此外，您的Adobe技术客户经理将为您提供此CDN的昵称。您需要将此别名作为Bootstrap URL中的参 `ptcdn` 数的值进行传递。

您可以通过Adobe支持在CRS端配置多个CDN。 但是，用于选择要通过清单服务器拼接广告资源的CDN必须是作为Bootstrap URL中参数值传递的CDN `ptcdn` 。
