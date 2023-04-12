---
title: 动态客户端注册
description: 动态客户端注册
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 动态客户端注册 {#dynamic-client-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 上下文 {#context}

为了与现代安全实践、改进的UX和平台所有者要求保持一致，Adobe Primetime身份验证Android SDK和iOS SDK正朝着采用的方向发展 [Android Chrome自定义选项卡](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

当前的AdobePass实施使用平台特定的Web视图，以便提供Web环境来显示MVPD登录页面。 这些Web视图与平台浏览器不共享凭据管理，因此在使用Adobe Primetime身份验证应用程序时，用户无法使用浏览器保存的密码。 此外，出于安全原因，一些平台正在弃用WebView控制器以执行身份验证任务。 Google和Apple均提供替代选项，如“Chrome自定义选项卡”和“Safari视图控制器”。 这些基本上是各自浏览器的单用选项卡。 Adobe Primetime身份验证将在2018年采用这些新组件。

## 详细信息 {#details}

目前，Adobe Pass身份验证可通过两种方式来识别和注册应用程序：

* 基于浏览器的客户端通过允许的域列表进行注册
* 本机应用程序客户端(如iOS和Android应用程序)通过签名请求者机制进行注册

为了解决Chrome自定义选项卡和Safari视图控制器的新流程，Adobe Pass提出了用于注册新应用程序的新客户端注册机制。 此机制将允许更安全、更精细地控制您的应用程序，并可用于在所有平台上注册应用程序。

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->