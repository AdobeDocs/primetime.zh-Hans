---
title: 集成您的广告服务器
description: 集成您的广告服务器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 集成您的广告服务器 {#integrate-ad-server}

首先，您需要登录以访问PrimetimeAd Insertion控制台，在该控制台中，您将设置PrimetimeAd Insertion用于将广告请求转发到您选择的广告服务器的规则。 PrimetimeAd Insertion支持大多数符合VAST或VMAP标准的广告服务器。

>[!NOTE]
>
>[IAB扩展页面](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## 宏支持 {#macro-support}

PrimetimeAd Insertion可为所有流启用以下ad server宏：

* Cache-busting
* 应用程序上下文或页面URL
* 可用持续时间
* 当前视频资产

如果需要其他宏，请联系您的Adobe Primetime支持代表。

## 高级功能 {#advanced-features}

PrimetimeAd Insertion还具有启用高级功能的基于规则的决策。 如果要根据库存权限将广告路由到不同的广告服务器，或者为各个广告启用频率封顶，这一点可能很重要。 有关更多信息，请参阅 [高级功能](/help/primetime-ad-insertion/advanced-features/route-ads-based-on-rules.md).
