---
title: 监控Adobe Primetime身份验证
description: 监控Adobe Primetime身份验证
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 监控Adobe Primetime身份验证 {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 介绍 {#intro}

客户可以使用 [纳吉奥斯](http://www.nagios.org) 或其他工具来检查Adobe Primetime身份验证是启动还是关闭。

## 监控端点 {#monitoring-endpoints}

### 可监视的端点 {#endpoints-to-monitor}

* 所有平台的配置端点： `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]` — 通过HTTP或HTTPS提供（取决于内容提供商的开发人员所做的选择）。 如果缺少此端点，则意味着您的内容将不可用于所有平台和所有MVPD。 对于无客户端REST API，我们还具有以下端点：  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* 以下端点是Adobe Primetime身份验证Web SDK的一部分。  如果缺少该参数，则意味着所有程序员和所有Web属性的pay-TVpass都将关闭：

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`


### 不应监视的端点 {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

  您始终会收到503错误，因为此端点需要一个MVPD SAML响应。

* 其他权利端点 —  `adobe-services/1.0/authenticate/`， `adobe-services/1.0/deviceShortAuthorize`， `adobe-services/1.0/authorize`

您无法监测这些端点，因为它们需要相关回复的有效负荷。
