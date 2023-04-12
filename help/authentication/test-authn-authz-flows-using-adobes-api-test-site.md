---
title: 如何使用Adobe的API测试网站测试身份验证和授权流程
description: 如何使用Adobe的API测试网站测试身份验证和授权流程
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# 如何使用Adobe的API测试网站测试身份验证和授权流程 {#How-to-test-auth-flows}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

为了测试AuthN和AuthZ流，我们准备了 **API测试网站** 你可以支配。 我们的支持团队将很乐意为您提供凭据。 您可以通过 **support@tve.zendesk.com**.


## 第一部分 {#part-I}

要针对RELEASE环境进行测试，请直接跳到第II部分。  要在资格预审环境中进行测试，请参阅 [在每季度前设置环境和测试](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

## 第二部分

完成第一部分后，执行以下步骤：


1. 开放网页： [测试API测试](https://sp.auth-staging.adobe.com/apitest/api.html).
1. 从以下URL加载访问启用码：
   * [访问用于暂存的启用程序javascript](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js).
   * 或
   * [访问用于生产的启用程序javascript](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
   * 然后，单击&#x200B;**Load Access Enabler**“ ”按钮。
1. 现在将请求者id值设置为“**requestorID**&quot; ，然后单击“setRequestor”按钮。
1. 然后，按“getAuthentication”按钮并等待显示选取器显示。
1. 选择“**MVPD**“ ”。
1. 在“**MVPD**“登录”页面。
1. 重定向回后，重做步骤1至3
1. 在“setAuthenticationStatus”上重新执行步骤3后，您应会看到值“1”。 如果身份验证不起作用，将显示MVPD对话框。
1. 要测试授权，请在资源输入字段中输入“**requestorID**&quot; ，然后单击“getAuthorization”按钮。
1. 因此，在“setToken” — \>“resource id”文本框中，将显示资源，在“setToken” — \>“token”文本框中，将显示shortAuthorizationToken，这表示authZ成功。
1. 现在，您可以单击“注销”按钮以删除令牌。

