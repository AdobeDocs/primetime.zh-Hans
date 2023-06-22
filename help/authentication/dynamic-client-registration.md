---
title: 动态客户端注册
description: 动态客户端注册
exl-id: 9bc2597d-b634-4542-849b-8e91a76cb8da
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 动态客户端注册 {#dynamic-client-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 上下文 {#context}

为了与现代安全实践、改进的UX和平台所有者要求保持一致，Adobe Primetime Authentication Android SDK和iOS SDK正在朝着采用方向发展 [Android Chrome自定义选项卡](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

当前AdobePass实施使用平台特定的Web视图，以提供用于显示MVPD登录页面的Web环境。 这些Web视图不会与平台浏览器共享凭据管理，因此用户在使用Adobe Primetime身份验证应用程序时无法使用浏览器保存的密码。 此外，出于安全原因，一些平台正逐渐弃用WebView控制器来执行身份验证任务。 Google和Apple都提供替代选项，如“Chrome自定义选项卡”和“Safari视图控制器”。 这些基本上是其各自浏览器的单一使用选项卡。 Adobe Primetime身份验证将在2018年采用这些新组件。

## 详细信息 {#details}

目前，Adobe Pass身份验证通过两种方式标识和注册应用程序：

* 基于浏览器的客户端通过允许的域列表进行注册
* 本机应用程序客户端(如iOS和Android应用程序)通过签名的请求者机制进行注册

为了解决Chrome自定义选项卡和Safari视图控制器的新流程，Adobe Pass提出了一种用于注册新应用程序的新客户端注册机制。 此机制将允许对应用程序进行更安全和精细的控制，并且可用于在所有平台上注册应用程序。

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
