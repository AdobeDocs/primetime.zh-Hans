---
description: 您可以设置参考实施以使用Adobe Analytics报表。
title: 配置Adobe Analytics报表
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 配置Adobe Analytics报表 {#configure-adobe-analytics-reporting}

您可以设置参考实施以使用Adobe Analytics报表。

参考实施可配置为使用Primetime SDK中捆绑的Adobe移动库将Primetime身份验证事件数据发送到Adobe Analytics。 要启用和使用从应用程序发送的事件数据，您必须首先创建一个Adobe Analytics帐户。 创建帐户后：

1. 使用您的帐户信息配置应用程序；以及
1. 创建处理规则以自定义事件数据在报表中的显示方式。

下表显示了发送到Adobe Analytics的数据：

| 操作名称 | `a.media.pass.event.MvpdSelection` | 用户在选择对话框中选择了多频道视频编程分发器(MVPD) |
|---|---|---|
| 上下文数据 | `a.media.pass.MvpdId (String)` | 用户选择的MVPD |
|  | `a.media.pass.ClientType` | （字符串）客户端类型为“flash”、“html5”、“ios”或“android” |
|  | | |
| 操作名称 | `a.media.pass.event.AuthenticationDetection` | 身份验证工作流已完成 |
| 上下文数据 | `a.media.pass.Successful` | （布尔值）令牌请求是否成功，true还是false |
|  | `a.media.pass.MvpdId` | （字符串）用户选择的MVPD |
|  | `a.media.pass.Guid` | （字符串）跟踪ID |
|  | `a.media.pass.Cached` | （布尔）令牌已在缓存中，为true或false |
|  | `a.media.pass.ClientType` | （字符串）客户端类型为“flash”、“html5”、“ios”或“android” |
|  | | |
| 操作名称 | `a.media.pass.event.AuthorizationDetection` | 授权工作流已完成 |
| 上下文数据 | `a.media.pass.Successful` | （布尔值）令牌请求是否成功，true还是false |
|  | `a.media.pass.MvpdId` | （字符串）用户选择的MVPD |
|  | `a.media.pass.Guid` | （字符串）跟踪ID |
|  | `a.media.pass.Cached` | （布尔）令牌已在缓存中，为true或false |
|  | `a.media.pass.Error` | （字符串）授权尝试失败时出错 |
|  | `a.media.pass.ErrorDetails` | （字符串）其他错误详细信息 |
|  | `a.media.pass.ClientType` | （字符串）客户端类型为“flash”、“html5”、“ios”或“android” |

1. 配置应用程序以用于Adobe Marketing Cloud。

   要启用将Primetime Primetime身份验证数据发送到Adobe Analytics，请 [!DNL `ADBMobileConfig.json`] 在编译时，必须将配置文件添加到参考实现中。 请注意，这是与Primetime SDK用于向Marketing Cloud发送Video Analytics数据的配置文件完全相同的配置文件。 请查阅 [Adobe Marketing Cloud文档](https://microsite.omniture.com/t2/help/en_US/reference/) 有关使用Adobe Analytics帐户配置应用程序的更多信息。
1. 创建处理规则。

   参考实施发送的Primetime身份验证事件数据不会自动显示在您的分析报表中。 您必须首先通过创建处理规则来使用数据。 请查阅 [有关创建处理规则的Adobe Analytics文档](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
