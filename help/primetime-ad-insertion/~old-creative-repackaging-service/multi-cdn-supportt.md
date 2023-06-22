---
description: 多CDN允许设置一个或多个CDN位置以提供转码广告。
title: 多CDN支持
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 多CDN支持 {#multi-cdn-support}

多CDN允许设置一个或多个CDN位置以提供转码广告。

默认情况下，所有转码资产都托管在Adobe拥有的Akamai CDN上。 但是，您可以自行选择零个或多个其他CDN位置，CRS将在这些位置托管转码资产。 因此，在这种情况下，您可以从同一CDN提供转码资源和内容。

当清单服务器查找转码请求时，它会使用包含大量查询参数的引导URL。 如果您设置了多CDN环境，则引导URL还需要包含 `ptcdn` parameter.manifest服务器使用此参数来标识从中获取广告转码版本的CDN服务器。

以下Primetime解决方案也支持多个CDN：

1. 适用于Android的TVSDK
1. 适用于桌面HLS的TVSDK
1. 适用于iOS的TVSDK

## 启用CDN支持 {#section_1BA344F2300B49F291865A7461EDFEAE}

默认情况下，为所有客户禁用CRS

请联系您的Adobe技术客户经理，将您的CRS帐户配置为使用其他CDN来托管转码广告资产。您需要提供以下CRS将转码广告资产上传到CDN所需的信息

1. CDN URL
1. 身份验证详细信息
1. 输出URL格式

此外，您的Adobe技术客户经理将为您提供此CDN的昵称。您需要将此昵称作为 `ptcdn` 参数BootstrapURL中的。

您可以通过Adobe支持在CRS端配置多个CDN。 但是，用于选取要通过清单服务器拼接的广告资产的CDN需要是作为 `ptcdn` 参数BootstrapURL中的。
