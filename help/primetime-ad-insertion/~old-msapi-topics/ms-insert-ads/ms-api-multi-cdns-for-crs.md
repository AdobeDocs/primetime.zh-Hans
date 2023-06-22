---
description: 虽然默认的Creative Repackaging Service (CRS)方案是使用一个Content Delivery Network (CDN)，但您可以在多个CDN上部署CRS资产。
title: 对CRS广告投放的多个CDN支持
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 对CRS广告投放的多个CDN支持 {#multiple-cdn-support-for-crs-ad-delivery}

虽然默认的Creative Repackaging Service (CRS)方案是使用一个Content Delivery Network (CDN)，但您可以在多个CDN上部署CRS资产。

## 要求

由于以下原因，您可以使用多个CDN：

* 需要针对大型查看事件进行扩展
* 将CRS资产的CDN源与主内容的CDN源进行匹配的要求。
* 需要使用与CRS默认CDN (Akamai)不同的CDN。

当清单服务器查找转码请求时，它会使用包含大量查询参数的引导URL。 如果您设置了多CDN环境，则引导URL还需要包含 `ptcdn` 参数。 清单服务器使用此参数来识别从中获取广告转码版本的CDN服务器。

有关更多详细信息，请参阅 [多CDN支持](../../~old-creative-repackaging-service/multi-cdn-supportt.md) ，位于CRS文档中。
