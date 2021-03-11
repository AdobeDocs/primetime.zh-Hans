---
description: 虽然默认的创意重新打包服务(CRS)方案是使用一个内容投放网络(CDN)，但您可以在多个CDN上部署CRS资源。
title: CRS广告投放的多个CDN支持
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 对CRS广告投放{#multiple-cdn-support-for-crs-ad-delivery}的多个CDN支持

虽然默认的创意重新打包服务(CRS)方案是使用一个内容投放网络(CDN)，但您可以在多个CDN上部署CRS资源。

## 要求

您可以出于以下原因使用多个CDN:

* 需要向上扩展以适合大型查看事件
* 要求将CRS资源的CDN源与主内容的CDN源匹配。
* 要求使用与CRS默认CDN(Akamai)不同的CDN。

当清单服务器查找转码请求时，它使用包含许多查询参数的引导URL。 如果已设置多CDN环境，则引导URL还需要包含`ptcdn`参数。 清单服务器使用此参数标识从中获取广告转码版本的CDN服务器。

有关详细信息，请参阅CRS文档中的[多CDN支持](../../~old-creative-repackaging-service/multi-cdn-supportt.md)。
