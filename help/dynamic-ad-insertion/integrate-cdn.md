---
title: 集成CDN
description: 集成CDN
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 集成CDN {#integrating-cdn}

PrimetimeAd Insertion充当客户端应用程序和清单之间的代理，而不是视频块本身。 将内容部署到所选CDN，并使用BootstrapAPI将URL传递到PrimetimeAd Insertion。<!-- For integration details, see [Supported CDNs](supported-cdns.md).-->

## 支持的CDN令牌化方案{#cdn-tokenization-schemes}

CDN通常具有不同的片段授权令牌化方案。 PrimetimeAd Insertion本机支持主要CDN网络，包括：

* Akamai
* Limelight
* Centurylink / Level3
* 要获得受支持CDN的完整列表，请与Primetime支持代表联系

有关`pttoken`参数的详细信息，请参阅[BootstrapAPI参数说明](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)。

## 将广告配置为从内容CDN {#configure-ad-deliver-from-cdn}投放

您可能希望从同一CDN投放广告和内容，以维护内容关联、帮助绕过广告拦截器和／或优化客户端应用程序所需的连接数。 PrimetimeAd Insertion支持片段重写规则，将片段映射到您的内容CDN。

<!--## Increase start-up performance with your CDN {#increase-startup-performance}

For more information, see [Optimizing start-up](optimize-video-startup-time.md).-->

## 多CDN功能{#enable-multi-cdn-fetures}

联系您的Primetime支持代表以启用多CDN功能。
