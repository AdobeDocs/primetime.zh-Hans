---
title: 设置Adobe PrimetimeAd Insertion
description: 设置Adobe PrimetimeAd Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 设置Adobe PrimetimeAd Insertion {#ptai-setup}

设置PrimetimeAd Insertion的流程如下：

1. 通过登录PrimetimeAd Insertion控制台并设置重定向规则，将广告服务器集成到PrimetimeAd Insertion中。 有关更多信息，请参阅 [集成广告服务器](/help/primetime-ad-insertion/getting-started/integrate-ad-server.md).

1. 在Primetime渠道控制台中配置Ad Insertion或平台，以确保有足够的报表维度。

1. 在PrimetimeAd Insertion中配置和集成CDN。 有关更多信息，请参阅 [集成CDN](integrate-cdn.md).

1. 确定广告工作流是否需要及时广告重新打包。 请联系您的Primetime支持代表以启用该服务。

1. 更新您的应用程序以使用 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) 发出和接收PrimetimeAd Insertion请求，并将您的应用程序配置为支持。 有关更多信息，请参阅 [广告跟踪](set-up-ad-tracking.md).

1. 测试您的应用程序以确保使用正确播放广告 [调试工具](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/troubleshoot-and-debug.md).

1. 使用测试您的应用程序以确保正确触发广告跟踪和展示信标 [报表](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/reporting-and-billing.md).
