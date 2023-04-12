---
title: 呈报程序
description: 呈报程序
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 呈报程序 {#escalation-procedures}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

>[!IMPORTANT]
> 
>致电热线： **+1-205-693-9813** 并发送电子邮件至 **tve-support@adobe.com** 包括 **紧急 — 事件** 在主题行中。

## 简介 {#introduction}

本文档介绍了重大事件的支持程序(**严重性1** 级别)影响Adobe Primetime身份验证、Primetime并发监控及其合作伙伴。\
 

## 严重性为1级事件的定义 {#definition-of-a-severity-1-level-incident}

A **严重性1** 级别事件是 **实时** 情况， **在生产环境中发生的事件**，这不允许完成一个渠道和一个MVPD的身份验证和/或授权流，从而影响执行该流的MVPD的大量用户。


## 严重性为1的事件示例 {#examples-of-severity-1-incidentcs}

* 托管在  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` (或 `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`)不可用。

* 对于特定的MVPD，在用户选择MVPD（在任何支持的浏览器中）后，Adobe不再重定向/显示登录页面。

* 合作伙伴收到大量报告，表明用户无法通过特定MVPD进行身份验证/授权。

* 在身份验证过程中，用户卡在Adobe错误页面上，无法重新启动身份验证/授权流程。


| 示例 **NOT** 严重性为1的事件 |
|---|
| 对于此类问题，Adobe将为调查提供支持，但它们不是严重级别为1的事件：<ul><li>由于Flash版本问题(缺少Flash、Flash阻止程序、Flash版本错误)，一个或多个订阅者无法执行流程。</li><li>一个或几个用户无法进行身份验证并保留在MVPD登录页面上。</li><li>一个或几个订阅者经过身份验证，但无法播放视频。</li><li>在程序员网站上，有/少/所有订阅者遇到JavaScript错误</li></ul> |

## 严重性为1的呈报流程 {#severity-1-escalation-flows}

严重性1事件可能由Adobe或Adobe Primetime身份验证合作伙伴发起。 每个步骤的步骤如下所示。

### 合作伙伴启动的流程 {#partner-initiated-flow}

1. 合作伙伴确定严重性为1的事件（如上所述），需要Adobe立即予以关注。
1. 合作伙伴向 **tve-support@adobe.com** 包括 **紧急 — 事件** 并添加以下信息：
   * 标题
   * 重现问题的说明和步骤
   * 操作系统/浏览器
   * SDK和版本
   * 受影响的设备
   * 受影响的用户百分比
   * HTTP跟踪或设备日志，用于说明问题
   * （可选）任何显示问题的可用屏幕截图或视频捕获
1. 如果Adobe在30分钟内未响应票证，则合作伙伴会调用以下号码：
   **1-205-693-9813**

   >[!IMPORTANT]
   >如果您在票证标题中未包含“URGENT-INCIDENT”，则我们的通知系统将不会接收该事件**。

### Adobe启动的流量 {#adobe-initiated-flow}

#### ...(针对Adobe Primetime身份验证问题) {#adobe-initiated-flow-authn-issue}

1. Adobe会识别内部问题，并通过我们的跟踪系统打开一个票证。

1. Adobe会通知合作伙伴的计划经理和技术联系人，以指定票证编号以及问题的预计影响。

1. Adobe致力于解决该事件，并随时向所有受影响的合作伙伴提供信息。

#### ...（程序员/MVPD） {#adobe-initiated-flow-partner-issue}

1. Adobe标识与MVPD集成或在某个程序员网站上集成相关的问题。

1. Adobe会通知受影响的合作伙伴 <u>遵循与该合作伙伴一起实施的支持程序</u> 并与合作伙伴的支持组织打开票证。

1. 如果在影响分析期间，Adobe确定问题属于事件情景中预先商定的决策之一，请参阅 **关于事件情景的预先商定决定**，它将相应地执行操作，而无需等待合作伙伴的投入。

1. Adobe将等待合作伙伴的更新以及恢复服务后合作伙伴的通知。

## 关于事件情景的预先商定决定 {#pre-agreed-descn}

在某些情况下，如果出现这种情况，将执行默认操作：

|  | 方案 | 描述 | 操作 |
|---|---|---|---|
| S1 | Adobe在正常生产操作期间标识MVPD集成的问题。 | 在正常生产操作期间，Adobe会发现其中一个MVPD存在的问题，该问题导致无法执行身份验证/授权流（例如，过期的证书、过期的SAML响应、端口关闭、更改的参数等） | -Adobe将通知受影响的MVPD和程序员。  </br> </br> -Adobe将为所有受影响的程序员停用此MVPD。 </br> </br> -Adobe将根据与MVPD商定的支持程序，通过MVPD开立票证 |
| S2 | Adobe为程序员激活新的MVPD，并且程序员在启动日期之前允许MVPD。 | Adobe正在为程序员网站激活新的MVPD，并且该网站已在选取器中显示新的MVPD，即使它本不应显示。 | -Adobe将在计划日期之前通知程序员在选取器中出现新的MVPD。 </br> </br>   — 程序员将在必要时从选取器中将其删除。 |
| S3 | Adobe可为程序员激活新的MVPD，即使MVPD尚未准备好投入生产 | Adobe正在为程序员激活新的MVPD，但MVPD尚未部署对集成的支持，因此无法执行身份验证/授权流 | -Adobe仅在程序员要求时才执行部署 </br> </br>  — 程序员将负责确保在所有测试完成后MVPD的许可。 |

## 严重级别为1的事件的响应预期 {#response-expectations-for-severity-one-incidents}

* 初始响应：30分钟(24/7)
* 行动计划：1小时(24/7)
* 解决办法：尽快(24/7)
