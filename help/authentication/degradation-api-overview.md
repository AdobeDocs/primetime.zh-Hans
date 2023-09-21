---
title: 降级API概述
description: 降级API概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 降级API概述 {#degradation-api-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 一般信息 {#general_info}

>[!NOTE]
>
>此API不公开发布。 有关可用性更新，请联系您的Adobe代表。

此功能使集成中的三大方(程序员、MVPD和Adobe)能够暂时绕过特定的MVPD身份验证和授权端点。 通常，是程序员发起此类操作，但无论谁触发了降级事件，该操作都取决于先前与受影响的MVPD商定的安排。

此功能的主要用例发生在直播体育或大型活动期间。 在此类高流量情况下，特定MVPD端点上的负载可能会变得过高，从而导致用户的响应时间非常长。 为了在这种情况下保持良好的用户体验，程序员可决定触发可临时自动验证/自动授权用户的降级规则，或通过从可用的MVPD列表中删除它来禁用MVPD。

降级规则仅应用于固定时间段。 虽然此功能的主要客户是体育频道和实时新闻频道，但任何程序员都可能希望能够访问此功能，因为MVPDs服务确实会不时地停止运转。

降级说明：

* 此功能旨在与使用监控API结合使用，后者提供有关每个MVPD的身份验证和授权数、平均授权延迟以及完整服务概述所需的其他量度的实时信息。
* 此功能不允许绕过AdobePrimetim身份验证服务。 如果Primetime身份验证处于关闭状态，则该服务中没有机制可用于允许用户查看内容。 但是，这些网站或应用程序可以自行绕过Primetime身份验证。
* Adobe当前不会直接触发性能降级 — 决策必须始终由已与MVPD同意此类条件的特定程序员作出。 将来，如果可以使用MVPD达成协议（SLA保护），Primetime身份验证可能会主动触发降级规则。

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
