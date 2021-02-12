---
description: Multi CDN允许设置一个或多个CDN位置以提供转码广告。
seo-description: Multi CDN允许设置一个或多个CDN位置以提供转码广告。
seo-title: 多CDN支持
title: 多CDN支持
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 多CDN支持{#multi-cdn-support}

Multi CDN允许设置一个或多个CDN位置以提供转码广告。

默认情况下，所有转码资源都托管在Adobe拥有的Akamai CDN上。 但是，您可以选择您自己的零个或多个附加CDN位置，CRS将在该位置托管转码资产。 因此，在这种情况下，可以从同一CDN提供转码资源和内容。

清单服务器查找转码请求时，它使用包含多个查询参数的引导URL。 如果已设置多CDN环境，引导URL还需要包含`ptcdn`参数。清单服务器使用此参数标识从中获取转码版本的广告的CDN服务器。

还提供以下Primetime解决方案的多CDN支持：

1. 适用于Android的TVSDK
1. 桌面HLS的TVSDK
1. iOS版TVSDK

## 启用CDN支持{#section_1BA344F2300B49F291865A7461EDFEAE}

默认情况下，CRS对所有客户都处于禁用状态

请与Adobe技术客户经理联系，将您的CRS帐户配置为使用其他CDN来托管转码广告资产。您需要提供CRS将转码广告资产上传到CDN所需的以下信息

1. CDN URL
1. 身份验证详细信息
1. 输出URL格式

此外，Adobe技术客户经理将为您提供此CDN的昵称。您需要将此昵称作为BootstrapURL中`ptcdn`参数的值进行传递。

您可以通过Adobe支持在CRS端配置多个CDN。 但是，用于选择要通过清单服务器拼接广告资源的CDN必须是作为BootstrapURL中`ptcdn`参数值传递的CDN。
