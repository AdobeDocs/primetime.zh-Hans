---
title: 授权服务监控概述
description: 授权服务监控概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# 授权服务监控概述 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#introduction}

TVE网站和应用程序需要24/7可用，因此客户需要实时分析权利事件，以便尽快发现和纠正问题。 他们还需要分析每月数据，以确定哪些平台提供了大量流量，哪些平台的实施情况可能不佳且转化率较低。

授权服务监控(ESM)为程序员和MVPD提供数据馈送，以便实时查看其身份验证和授权事件。 数据从Adobe Primetime身份验证系统收集，并通过RESTful API提供。  客户可以直接使用数据，也可以从他们自己自定义的操作功能板中使用数据。

ESM系统的核心要素是其指标和维度。 ESM根据维度选择生成包含聚合量度的报表。 当Adobe Pass事件以PST时区记录时，ESM报告也以PST时区提供。 

ESM API通常不可用。  有关可用性问题，请联系您的Adobe代表。

## 面向程序员的ESM {#esm-for-programmers}

### 程序员可以监控以下量度： {#programmers-monitor-metrics}


| *量度名称* | *描述* |
|-------------------------|--------------------------|
| authn-attempts | 启动的身份验证流数 |
| authn-successful | 客户端成功获取的身份验证令牌数量 |
| authn-pending | 成功生成的身份验证令牌数量（无论客户端是否实际获取了该令牌） |
| authn-failed | 通过外部系统执行的失败身份验证数。 |
| 无客户端令牌 | 已成功发出无客户端令牌的数量 |
| 无客户端故障 | 尝试从无客户端API接收令牌失败的次数 |
| authz-attempts | 尝试的授权数 |
| authz successful | 成功授权的数量 |
| authz-failed | MVPD在应用程序级别拒绝的授权数 |
| authz-rejected | 由于DoS攻击预防而被Adobe服务提供商视为恶意并被拒绝的授权尝试次数 |
| authz-latency | 在MVPD端点上花费的总毫秒数 |
| media-tokens | 生成的短媒体令牌数（与播放请求数同化） |
| 独特帐户 | 在选定时间间隔内执行授权(AuthN / AuthZ)操作的独特用户数。 （此量度仅在请求每日值时才显示。） </br> 这是针对每个数据中心计算的。 未请求“dc”维度时，将不显示此量度。 |
| 独特会话 | 在选定时间间隔内对Adobe Primetime身份验证服务执行身份验证流程调用的唯一会话数。 （此量度仅在请求每日值时才显示。） </br> 这是针对每个数据中心计算的。 未请求“dc”维度时，将不显示此量度。 |
| 计数 | 面向事件的报表中使用的简单计数器 |

</br>

### 程序员可以按以下维度过滤上述量度： {#progr-filter-metrics}


| *Dimension名称* | *描述* |
|---|---|
| 年 | 4位数年份 |
| 月份 | 月份(1-12) |
| 天 | 当月(1-31) |
| 小时 | 一天中的小时 |
| 分钟 | 小时的分钟 |
| media-company | 拥有启动用户授权流程的网站的媒体公司 |
| dc | （数据中心）收到请求的主区域。 |
| 代理 | 代理MVPD（将“直接”用于直接集成） |
| mvpd | 负责向用户授予权限的MVPD |
| requestor-id | 用于执行授权请求的请求者ID |
| 频道 | 从资源字段提取的渠道网站（如果提供，则从MRSS有效负载提取为渠道/标题，或者如果它不是RSS格式，则映射到资源值）。 |
| resource-id | 授权请求中涉及的实际资源标题（如果提供，则从MRSS有效负载中提取为项目/标题） |
| 设备 | 设备平台（PC、移动设备、控制台等） |
| eap | 当通过外部系统执行验证流时，外部验证提供器。 </br> 值可以是： </br>  — 不适用 — 身份验证由Primetime身份验证提供 </br> - Apple — 提供身份验证的外部系统为Apple |
| os系列 | 在设备上运行的操作系统 |
| 浏览器系列 | 用于访问Adobe Primetime身份验证的用户代理 |
| cdt | 当前用于无客户端的设备平台（替代）。 </br>  值可以是： </br>  — 不适用 — 事件并非源自无客户端SDK </br>  — 未知 — 由于无客户端API中的deviceType参数是可选的，因此有一些调用不包含任何值。 </br>  — 通过无客户端API发送的任何其他值，如xbox、appletv、roku等。 </br> |
| platform-version | 无客户端SDK的版本 |
| os-type | 在设备上运行的操作系统，备用（当前未使用） |
| browser-version | 用户代理版本 |
| sdk-type | 使用的客户端SDK(Flash、HTML5、Android本机、iOS、无客户端等) |
| sdk-version | Adobe Primetime身份验证客户端SDK的版本 |
| 事件 | Adobe Primetime身份验证事件名称 |
| 原因 | 失败的原因(由Adobe Primetime身份验证报告) |
| sso-type | 底层SSO机制：platform/passive/adobe. 表示授权令牌是通过在其他应用程序中重用AuthN而发出的 |

## 适用于MVPD的ESM {#esm-for-mvpds}

### MVPD可以监控以下量度：

| *量度名称* | *描述* |
|---|---|
| authn-attempts | 启动的身份验证流数 |
| authn-successful | 客户端成功获取的身份验证令牌数量 |
| authn-pending | 成功生成的身份验证令牌数量（无论客户端是否实际获取了该令牌） |
| authn-failed | 通过外部系统执行的失败身份验证数。 |
| authz-attempts | 尝试的授权数 |
| authz successful | 成功授权的数量 |
| authz-failed | MVPD在应用程序级别拒绝的授权数 |
| authz-rejected | 由于DoS攻击预防而被Adobe服务提供商视为恶意并被拒绝的授权尝试次数 |
| authz-latency | 在MVPD端点上花费的总毫秒数 |

### MVPD可以按以下维度过滤上面列出的量度：

| *Dimension名称* | *描述* |
|---|---|
| 年 | 4位数年份 |
| 月份 | 月份(1-12) |
| 天 | 当月(1-31) |
| 小时 | 一天中的小时 |
| 分钟 | 小时的分钟 |
| requestor-id | 用于执行授权请求的请求者ID |
| eap | 当通过外部系统执行验证流时，外部验证提供器。 </br> 值可以是： </br>  — 不适用 — 身份验证由Primetime身份验证提供 </br> - Apple — 提供身份验证的外部系统为Apple |
| cdt | 当前用于无客户端的设备平台（替代）。 </br>  值可以是： </br>  — 不适用 — 事件并非源自无客户端SDK </br>  — 未知 — 由于无客户端API中的deviceType参数是可选的，因此有一些调用不包含任何值。 </br>  — 通过无客户端API发送的任何其他值，如xbox、appletv、roku等。 </br> |
| sdk-type | 使用的客户端SDK(Flash、HTML5、Android本机、iOS、无客户端等) |


## 用例 {#use-cases}

您可以将ESM数据用于以下用例：

- **监控**  — 运营或监控团队可以创建每分钟调用API的功能板或图表。 使用显示的信息，他们可以在出现问题时（通过Primetime身份验证或通过MVPD）检测到问题。  

- **调试/质量测试**  — 由于数据也按平台、设备、浏览器和操作系统进行划分，因此分析使用模式可以发现特定组合（例如，OSX上的Safari）上的问题。  

- **Analytics**  — 提供的数据可用于补充/审核通过Adobe Analytics或其他分析工具收集的客户端数据。

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->