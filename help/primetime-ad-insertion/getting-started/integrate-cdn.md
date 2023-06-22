---
title: 集成您的CDN
description: 集成CDN
exl-id: b93031a2-6e66-4de1-9cf2-b0260f88fe13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 集成您的CDN {#integrating-cdn}

PrimetimeAd Insertion充当客户端应用程序和清单之间的代理，而不是视频块本身。 将您的内容部署到所选的CDN，并使用BootstrapAPI将URL传递到PrimetimeAd Insertion。 有关集成的详细信息，请参阅 [支持的CDN](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## 支持的CDN令牌化方案 {#cdn-tokenization-schemes}

CDN通常具有不同的片段授权令牌化方案。 PrimetimeAd Insertion本机支持主要的CDN网络，包括：

* Akamai
* Limelight
* Centurylink /级别3
* 有关支持的CDN的完整列表，请与Primetime支持代表联系

欲知关于 `pttoken` 参数，请参见 [BootstrapAPI参数描述](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## 配置要从内容CDN投放的广告 {#configure-ad-deliver-from-cdn}

您可能希望从同一CDN投放广告和内容以保持内容亲和度，帮助绕过广告拦截器和/或优化来自客户端应用程序的所需连接数。 PrimetimeAd Insertion支持片段重写规则，以将片段映射到您的内容CDN。 有关更多信息，请参阅 [清单重写](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## 利用CDN提高启动性能 {#increase-startup-performance}

有关更多信息，请参阅 [优化启动](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## 多CDN功能 {#enable-multi-cdn-fetures}

请联系您的Primetime支持代表以启用多CDN功能。
