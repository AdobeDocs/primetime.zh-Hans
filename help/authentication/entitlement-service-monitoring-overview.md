---
title: 授权服务监控概述
description: 授权服务监控概述
exl-id: ebd5d650-0a32-4583-9045-5156356494e2
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# 授权服务监控概述 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 介绍 {#introduction}

TVE网站和应用程序需要全天候可用，因此客户需要实时洞察授权事件，以尽快检测和纠正问题。 他们还需要分析每月数据，以确定哪些平台提供了大部分流量，以及哪些平台可能实施不良、转化率低。

授权服务监控(ESM)为程序员和MVPD提供数据馈送，以便实时查看其身份验证和授权事件。 数据从Adobe Primetime身份验证系统中收集，并通过RESTful API提供。  客户可以通过直接方式使用数据，或从他们自己的自定义操作功能板中使用数据。

ESM系统的核心元素是其量度和维度。 ESM会根据维度选择生成包含汇总量度的报表。 由于Adobe Pass事件是以PST时区记录的，因此ESM报告也以PST时区提供。 

ESM API不公开发布。  有关可用性问题，请联系您的Adobe代表。

## 面向程序员的ESM {#esm-for-programmers}

### 程序员可以监控以下量度： {#programmers-monitor-metrics}


| *量度名称* | *描述* |
|-------------------------|--------------------------|
| authn-attempts | 启动的身份验证流的数量 |
| 验证成功 | 客户端成功获取的身份验证令牌数量 |
| authn-pending | 成功生成的身份验证令牌的数量（无论客户端是否实际获取它） |
| authn失败 | 通过外部系统执行的身份验证失败的次数。 |
| 无客户端令牌 | 已成功发出的无客户端令牌数量 |
| 无客户端故障 | 尝试从无客户端API接收令牌的失败次数 |
| authz-attempts | 尝试的授权数量 |
| authz成功 | 成功的授权数量 |
| authz-failed | 应用程序级别的MVPD拒绝的授权数 |
| authz-rejected | 由Adobe服务提供商视为恶意并因DoS攻击预防而拒绝的授权尝试次数 |
| authz-latency | 在MVPD端点上花费的总毫秒数 |
| media-tokens | 生成的短媒体令牌数量（与播放请求的数量相同） |
| 独特帐户 | 在所选时间间隔内执行授权(AuthN / AuthZ)操作的独特用户数。 （此量度仅在请求每日值时显示。） </br> 这是为每个单独的数据中心计算的。 当未请求“dc”维度时，将不显示此量度。 |
| 独特会话 | 在所选时间间隔内对Adobe Primetime身份验证服务执行身份验证流调用的唯一会话数。 （此量度仅在请求每日值时显示。） </br> 这是为每个单独的数据中心计算的。 当未请求“dc”维度时，将不显示此量度。 |
| count | 面向事件的报表中使用的简单计数器 |

</br>

### 程序员可以按以下维度筛选上面列出的量度： {#progr-filter-metrics}


| *Dimension名称* | *描述* |
|---|---|
| 年 | 4位数的年份 |
| 月 | 月份(1-12) |
| 天 | 日期(1-31) |
| 小时 | 一天中的第几个小时 |
| 分钟 | 小时中的分钟 |
| media-company | 拥有启动用户权利流程的网站的媒体公司 |
| dc | （数据中心）收到请求的主区域。 |
| 代理 | 代理MVPD（对于直接集成，它将是“直接”的） |
| mvpd | 负责授予用户权利的MVPD |
| requestor-id | 用于执行授权请求的请求者ID |
| 渠道 | 渠道网站，从资源字段提取（从MRSS有效负载提取作为渠道/标题，如果提供，或者映射到资源值，如果它不是RSS格式）。 |
| resource-id | 授权请求中涉及的实际资源标题（从MRSS有效负载提取为项目/标题，如果提供） |
| 设备 | 设备平台（PC、移动设备、控制台等） |
| eap | 通过外部系统执行身份验证流程时的外部身份验证提供程序。 </br> 值可以是： </br> - N/A — 身份验证由Primetime身份验证提供 </br> - Apple — 提供身份验证的外部系统是Apple |
| os系列 | 设备上运行的操作系统 |
| browser-family | 用于访问Adobe Primetime身份验证的用户代理 |
| cdt | 当前用于无客户端的设备平台（替代）。 </br>  值可以是： </br> - N/A — 事件不是源自无客户端SDK </br>  — 未知 — 由于无客户端API中的deviceType参数是可选的，因此有些调用不包含任何值。 </br>  — 通过无客户端API发送的任何其他值，例如xbox、appletv、roku等。 </br> |
| platform-version | 无客户端SDK的版本 |
| 操作系统类型 | 设备上运行的操作系统，替代方案（当前未使用） |
| browser-version | 用户代理版本 |
| sdk-type | 使用的客户端SDK(Flash、HTML5、Android native、iOS、无客户端SDK等) |
| sdk-version | Adobe Primetime身份验证客户端SDK的版本 |
| 事件 | Adobe Primetime身份验证事件名称 |
| 原因 | 失败的原因，由Adobe Primetime身份验证报告 |
| sso类型 | 底层SSO机制：platform/passive/adobe。 指示授权令牌是通过在其他应用程序中重复使用AuthN发出的 |

## MVPD的ESM {#esm-for-mvpds}

### MVPD可以监控以下度量：

| *量度名称* | *描述* |
|---|---|
| authn-attempts | 启动的身份验证流的数量 |
| 验证成功 | 客户端成功获取的身份验证令牌数量 |
| authn-pending | 成功生成的身份验证令牌的数量（无论客户端是否实际获取它） |
| authn失败 | 通过外部系统执行的身份验证失败的次数。 |
| authz-attempts | 尝试的授权数量 |
| authz成功 | 成功的授权数量 |
| authz-failed | 应用程序级别的MVPD拒绝的授权数 |
| authz-rejected | 由Adobe服务提供商视为恶意并因DoS攻击预防而拒绝的授权尝试次数 |
| authz-latency | 在MVPD端点上花费的总毫秒数 |

### MVPD可以按以下维度筛选上面列出的量度：

| *Dimension名称* | *描述* |
|---|---|
| 年 | 4位数的年份 |
| 月 | 月份(1-12) |
| 天 | 日期(1-31) |
| 小时 | 一天中的第几个小时 |
| 分钟 | 小时中的分钟 |
| requestor-id | 用于执行授权请求的请求者ID |
| eap | 通过外部系统执行身份验证流程时的外部身份验证提供程序。 </br> 值可以是： </br> - N/A — 身份验证由Primetime身份验证提供 </br> - Apple — 提供身份验证的外部系统是Apple |
| cdt | 当前用于无客户端的设备平台（替代）。 </br>  值可以是： </br> - N/A — 事件不是源自无客户端SDK </br>  — 未知 — 由于无客户端API中的deviceType参数是可选的，因此有些调用不包含任何值。 </br>  — 通过无客户端API发送的任何其他值，例如xbox、appletv、roku等。 </br> |
| sdk-type | 使用的客户端SDK(Flash、HTML5、Android native、iOS、无客户端SDK等) |


## 用例 {#use-cases}

您可以将ESM数据用于以下用例：

- **监测**  — 操作或监控团队可以创建每分钟调用API的功能板或图表。 使用显示的信息，他们可以在出现问题的一分钟就检测到问题（使用Primetime身份验证或MVPD）。  

- **调试/质量测试**  — 由于数据还按平台、设备、浏览器和操作系统进行划分，因此分析使用模式可以查明特定组合上的问题（例如OSX上的Safari）。  

- **分析**  — 提供的数据可用于补充/审核通过Adobe Analytics或其他分析工具收集的客户端数据。

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
