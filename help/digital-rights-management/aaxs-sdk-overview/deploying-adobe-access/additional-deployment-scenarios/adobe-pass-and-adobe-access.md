---
title: Adobe Pass和Adobe Access
description: Adobe Pass和Adobe Access
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Adobe Pass和Adobe Access {#adobe-pass-and-adobe-access}

Adobe Pass([](https://www.adobe.com/products/adobepass/))提供跨多个内容提供商的用户/设备身份验证和授权。 用户必须具有有效的有线电视或卫星电视订阅。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass可与Adobe Access一起使用，以保护媒体内容。 在此方案中，视频播放器(SWF)可以加载另一个SWF，称为由Adobe Systems托管的&#x200B;*访问启用程序*。 *访问启用程序*&#x200B;用于连接到Adobe Pass服务，并促进与MVPD（多通道视频编程分发商）标识提供者系统的SAML SSO集成。 这包括将用户的浏览器短暂重定向到MVPD登录页，然后保持AuthN令牌，最后使用缓存的AuthN会话返回到内容网站。

然后，*访问启用程序*&#x200B;便于在Adobe Pass服务和MVPD之间执行后端授权。 MVPD维护业务逻辑，并确定用户有权访问哪些内容。 授权将保留在该内容资源的其他AuthZ令牌中，并发送回客户端。

使用Adobe访问客户端的唯一ID和私钥对身份验证和授权令牌进行签名，以避免篡改或欺骗。 此令牌只能通过&#x200B;*访问启用程序*&#x200B;访问。

视频播放器可以通过调用&#x200B;*访问启用程序*&#x200B;上的`getAuthorization`来触发该过程。 当存在有效的AuthN/AuthZ令牌时，*AccessEnabler*&#x200B;将向视频播放器发出回调，该视频播放器将包含用于播放视频内容的短时媒体令牌。

Adobe Pass提供可部署到服务器的媒体令牌验证程序Java库。 当使用Flass Access服务器进行内容保护时，您可以将媒体令牌验证程序与Adobe Access服务器端插件集成，以在成功验证媒体令牌后自动发布通用许可证。 然后，内容会从CDN服务器流式传输到客户端。 为了获得内容许可证，可将短期媒体令牌提交到Adobe访问服务器，其中验证令牌的有效性并可以颁发许可证。

*访问启用程序*&#x200B;通常在所有内容开发者中使用长期AuthN令牌来表示该MVPD订阅者的AuthN。 此外，Adobe Access Server和令牌验证器可以由CDN或代表内容提供商的服务提供商运行。
