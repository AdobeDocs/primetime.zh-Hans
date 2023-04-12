---
title: 降级API概述
description: 降级API概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 降级API概述 {#degradation-api-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 一般信息 {#general_info}

>[!NOTE]
>
>此API通常不可用。 有关可用性更新，请联系您的Adobe代表。

此功能为集成(程序员、MVPD和Adobe)中的三大方中的任意一方提供了临时绕过特定MVPD身份验证和授权端点的功能。 通常是程序员模拟此类行动，但无论由谁触发降级事件，该行动都取决于先前与受影响的MVPD达成的安排。

此功能的主要用例发生在实时体育或大型活动期间。 在这种高流量情况下，特定MVPD端点上的负载可能会变得过高，从而导致用户响应时间过长。 为了在这种情况下保持良好的用户体验，程序员可决定触发可临时自动验证/自动授权用户的降级规则，或通过从可用的MVPD列表中将其删除来禁用MVPD。

退化规则仅应用于固定时间段。 尽管此功能的主要客户是体育频道和实时新闻频道，但是任何程序员都可能希望能够访问此功能，因为MVPD服务会不时地停止访问。

降级说明：

* 此功能旨在与使用情况监控API结合使用，该API可提供有关每个MVPD的身份验证和授权数量、平均授权延迟以及完整服务概述所需的其他量度的实时信息。
* 此功能不允许绕过Adobe期间身份验证服务。 如果Primetime身份验证处于下方，则服务中没有可用于允许用户查看内容的机制。 但是，网站或应用程序可以自行绕过Primetime身份验证。
* Adobe当前不会直接触发降级 — 此决定必须始终由与MVPD同意此类条件的特定程序员决定。 将来，如果可以通过MVPD达成协议（SLA保护），则Primetime身份验证可能会主动触发降级规则。

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->