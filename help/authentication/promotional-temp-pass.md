---
title: 促销临时传递
description: 促销临时传递
exl-id: 705c1ba9-0430-4e3b-add1-d9e4da3f82d1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---

# 促销临时传递 {#promotional-temp-pass}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 功能摘要 {#feature-summary}

促销临时密码允许程序员为没有MVPD帐户凭据的用户提供对其受保护内容的临时访问权限。

促销临时通行证设计用于运行促销活动，其中用户在向程序员提供有效的标识信息（例如电子邮件地址）之后，将能够使用 **在预定义的时间段内不同VOD标题的预定义数量**.

>[!IMPORTANT]
>
>Adobe不会存储任何个人身份信息(PII)。 因此，程序员必须对Primetime身份验证API上唯一用户提供的信息设置哈希。

促销临时通行证构建于 [临时传递](/help/authentication/temp-pass.md) 功能，这意味着它包含所有“临时传递”功能。

一旦超过最大预定义VOD标题数或预定义的时间段，该用户将无法访问同一设备上的内容或使用相同的用户标识符信息（例如，电子邮件地址），直到从Adobe Primetime身份验证服务器清除授权令牌为止。

>[!NOTE]
>
>临时传递是Premium Workflow包的一部分。 如果您有兴趣使用此功能，请联系您的Primetime销售代表。

## 临时通行证和促销临时通行证比较 {#tp-ptp-comparison}

| 临时传递 | 促销临时传递 |
|----------------------------------|----------------------------------------------------------------------------------------|
| 访问内容 <ul><li>基于时间</li></ul> | 访问内容 <ul><li>基于时间</li><li>基于资源数量</li></ul> |
| 访问安全性基于 <ul><li>设备Id</li></ul> | 安全性基于 <ul><li>设备Id</li><li>散列提供的用户标识符信息（例如，电子邮件）</li></ul> |
| 客户端错误API可用 | 客户端错误API可用 |
| 重置/清除可用 | 重置/清除可用 |

## 功能详细信息 {#feature-details}

此功能使用户在程序员应用程序中提供了唯一信息（如电子邮件地址）之后，可以从特定设备（电话和平板电脑）访问促销内容。

程序员将在身份验证和授权API上提供用户PII上的哈希。 此哈希将与设备ID结合使用，以生成用于标识用户和设备的唯一密钥。

Adobe Primetime身份验证将根据设备ID和用户提供的信息并按照以下逻辑判断用户是在新试用版中还是在现有试用版中：

* 对用户提供的信息进行新哈希（例如，电子邮件），新设备ID =>新试用
* 现有针对用户提供的信息的哈希（例如，电子邮件），新设备ID =>现有试用(具有现有针对用户提供的信息的哈希（例如，电子邮件）)
* 对用户提供的信息新增哈希（例如，电子邮件），现有设备ID =>现有试用版（具有现有设备ID）
* 现有散列覆盖用户提供的信息（例如，电子邮件），现有设备ID =>现有试用版

>[!NOTE]
>对用户提供的信息进行验证和哈希处理由程序员处理，而非Adobe。

**可根据以下属性配置“促销临时通过”功能：**

* 用户提供的信息密钥（例如，电子邮件）
* 用户有权使用的资源数
* TTL — 用户有权使用配置数量的资源的时间范围

### 用户元数据 {#user-metadata}

为便于实施程序员应用程序，请完成以下操作 **用户元数据信息公开** 促销临时通行证上，使用相应的键(要激活键，请联系tve-support@adobe.com)：

* **remain_resources**：当前用户有权使用的剩余资源数
* **used_assets**：当前用户已使用的资源列表
* **expiration_date**：当前用户的到期日期

### 如何计算观看时间？ {#compute-viewing-time}

临时通行证保持有效的时间与用户查看程序员应用程序上的内容所花费的时间无关。 在通过“提升临时通过”的授权初始用户请求时，通过将初始当前请求时间添加到由程序员指定的TTL（持续时间时间范围）来计算过期时间。

### 身份验证和授权 {#authn-authz}

对于“促销临时传递”流程，身份验证和授权不会与实际MVPD通信， **因此，所有授权请求都将成功** 只要满足以下所有条件：

* 授权令牌对指定资源有效
* 数量 **used_assets** 低于程序员设置的限制
* **expiration_date** 值晚于当前日期。

### 预检行为 {#preflight-beh}

当对促销临时通道MVPD发出预检或预授权请求时，返回的相应预检响应将包含来自预检请求的整个资源列表，因为预检成功。

其背后的逻辑是：“促销临时通过”授权条件基于时间和资源数量限制，而不是基于特定资源。 更具体地说，只要满足时间限制并且没有超过资源限制，被调用资源就将被授权。

### SSO {#sso}

Promotional Temp Pass实例未启用SSO，该实例配置为启用“每个请求者的身份验证”。 这意味着当用户从应用程序A切换到与同一促销临时密码集成的其他应用程序B时，用户不会自动登录。

### 注销 {#logout}

注销时会删除设备上的所有令牌。 因此，从“促销临时传递”切换到用户选择的常规MVPD不应依赖此实施。 建议使用 `setSelectedProvider(null)` 功能上是为了清除应用程序状态后重新启动身份验证流程，这有更好的用户体验。

### 提升临时传递流程图 {#promo-tempass-flowdia}

![提升临时传递流程图](assets/promo-temp-pass-flow.png)

*图：促销临时传递流程*

## 实施促销临时传递 {#impl-promo-tempass}

促销临时传递需要以下客户端功能：

* **用户标识符信息，例如电子邮件地址传播** （在身份验证和授权流程中发送用户的电子邮件地址）。 Adobe Primetime身份验证需要电子邮件来绑定身份验证和授权令牌(与 `device_ID`，在所有调用中必需)。
* **强制身份验证**  — 允许程序员在用户已经过身份验证后强制进行身份验证流程。 要强制用户元数据刷新（用户元数据键），需要使用此功能 **used_assets** 包含可用资源的数量)。 由于用户可以在多个设备上登录，因此设备上的用户元数据在应用程序启动期间不可靠，我们需要更新元数据以反映该特定用户的当前状态（由电子邮件地址标识）。


>[!IMPORTANT]
>仅可在iOS和Android上执行强制身份验证。
>Primetime身份验证没有内置机制可在X分钟后停止免费流式传输。 Primetime身份验证将停止发布 **授权** 和 **短媒体** 用户使用Y空闲资源后的令牌。 在“促销临时通过”过期后，将由程序员限制访问。

## 安全性 {#security}

>[!IMPORTANT]
>Adobe不会存储任何个人身份信息(PII)。 因此，程序员必须对Primetime身份验证API上唯一用户提供的信息设置哈希。

**用户标识符信息的哈希处理**

Adobe建议使用 **SHA-2** 家庭或其特定 **SHA-256**， **SHA-512** 在将数据发送到Adobe之前对数据执行各种函数。

例如， **SHA-256** 超过 **&quot;user@domain.com&quot;** 是 **“f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7”**.

## 重置或清除促销临时传递 {#reset-promo-tempass}

某些业务规则需要定期清除“促销临时通行证”。 为此，Primetime身份验证为程序员提供了 *公共* web API，如下所述：

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>协议： **https**</li><li>主机：<ul><li>版本： **mgmt.auth.adobe.com**</li><li>先决条件： **mgmt-prequal.auth.adobe.com**</li></ul></li><li>路径： **/reset-tempass/v2/reset**</li><li>查询参数： **device_id=all&amp;requestor_id=THE_REQUESTOR_ID&amp;mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>标头： ApiKey： **1232293681726481**</li> <li>响应：<ul><li>成功： **HTTP 204**</li><li>失败： **HTTP 400** 对于不正确的请求， **HTTP 401** 如果未指定ApiKey， **HTTP 403** 如果ApiKey无效</li></ul></li></ul> |

除了清除“临时传递”的要求之外，“促销临时传递”还使用发送的用户标识符信息的哈希值 **generic_data** 进行身份验证和授权以便清除。

将发送哈希，而不是整个JSON：

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"
```

### 支持的客户端 {#supported-clients}

| Adobe Primetime身份验证客户端 | 促销临时传递 | 重置工具 | 支持专用响应代码/客户端错误 |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| JS Access Enabler | 是 | 是 | 是（从v 3.0.0开始） |
| Native Client iOS | 是 | 是 | 是（从v 1.10开始） |
| Native Client Android | 是 | 是 | 是 |
| 无客户端API | 是 | 是 | 否 |


## 限制 {#limitations}

本节介绍适用于当前实施的促销临时通行证的限制。

### 无客户端 {#lim-clientless}

**没有唯一设备ID的智能设备**

并非所有智能设备应用程序都能提供唯一设备ID。 如果没有设备标识，Adobe Primetime身份验证可以使用Adobe注册代码服务生成的UUID作为唯一设备ID。 这意味着当用户注销时，身份验证和授权令牌将被删除。 一旦用户再次尝试进行身份验证，这次使用不同的用户信息（例如，电子邮件）用户将能够再次授权。 Adobe建议添加不允许用户“欺骗”系统的UI流程，并添加逻辑以确定是新用户请求试用还是现有试用。

**重置/清除临时传递**

在Xbox360和Xbox One的特定情况下，无法重置无客户端临时通道，因为这些平台需要额外的设备ID解析，在“重置临时通道”工具中无法实现。

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->
