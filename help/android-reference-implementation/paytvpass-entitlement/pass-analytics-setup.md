---
description: 您可以设置参考实施以使用Adobe Analytics报告。
seo-description: 您可以设置参考实施以使用Adobe Analytics报告。
seo-title: 配置Adobe Analytics报告
title: 配置Adobe Analytics报告
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 配置Adobe Analytics报告{#configure-adobe-analytics-reporting}

您可以设置参考实施以使用Adobe Analytics报告。

参考实施配置为使用绑定在Primetime SDK中的事件移动库将Primetime身份验证Adobe数据发送到Adobe Analytics。 要启用和使用从应用程序发送的事件数据，您必须先创建一个Adobe Analytics帐户。 创建帐户后：

1. 使用您的帐户信息配置应用程序；和
1. 创建处理规则以自定义事件数据在报表中的显示方式。

下表列出了发往Adobe Analytics的数据：

| 操作名称 | `a.media.pass.event.MvpdSelection` | 用户在选择对话框中选择了多渠道视频编程分配器(MVPD) |
|---|---|---|
| 上下文数据 | `a.media.pass.MvpdId (String)` | 用户选择的MVPD |
|  | `a.media.pass.ClientType` | （字符串）客户端类型为“flash”、“html5”、“ios”或“android” |
|  |  |  |
| 操作名称 | `a.media.pass.event.AuthenticationDetection` | 身份验证工作流已完成 |
| 上下文数据 | `a.media.pass.Successful` | （布尔值）令牌请求是成功、true还是false |
|  | `a.media.pass.MvpdId` | （字符串）用户选择的MVPD |
|  | `a.media.pass.Guid` | （字符串）跟踪ID |
|  | `a.media.pass.Cached` | （布尔值）已在缓存中的令牌，为true或false |
|  | `a.media.pass.ClientType` | （字符串）客户端类型为“flash”、“html5”、“ios”或“android” |
|  |  |  |
| 操作名称 | `a.media.pass.event.AuthorizationDetection` | 已完成授权工作流 |
| 上下文数据 | `a.media.pass.Successful` | （布尔值）令牌请求是成功、true还是false |
|  | `a.media.pass.MvpdId` | （字符串）用户选择的MVPD |
|  | `a.media.pass.Guid` | （字符串）跟踪ID |
|  | `a.media.pass.Cached` | （布尔值）已在缓存中的令牌，为true或false |
|  | `a.media.pass.Error` | （字符串）授权尝试失败时出错 |
|  | `a.media.pass.ErrorDetails` | （字符串）更多错误详细信息 |
|  | `a.media.pass.ClientType` | （字符串）客户端类型为“flash”、“html5”、“ios”或“android” |

1. 配置应用程序以与Adobe Marketing Cloud一起使用。

   要启用向Adobe Analytics发送Primetime身份验证数据，必须在编译时将[!DNL `ADBMobileConfig.json`]配置文件添加到参考实施。 请注意，这与Primetime SDK用于向Marketing Cloud发送视频分析数据的配置文件完全相同。 有关使用您的Adobe Marketing Cloud帐户配置应用程序的详细信息，请查阅[Adobe Analytics文档](https://microsite.omniture.com/t2/help/en_US/reference/)。
1. 创建处理规则。

   由“参考实施”发送的Primetime身份验证事件数据不会自动显示在您的分析报告中。 必须首先通过创建处理规则来利用数据。 请查阅有关创建处理规则的[Adobe Analytics文档](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html)。
