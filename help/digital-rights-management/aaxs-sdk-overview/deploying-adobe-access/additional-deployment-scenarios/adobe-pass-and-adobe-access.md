---
title: Adobe Pass和Adobe访问权限
description: Adobe Pass和Adobe访问权限
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Adobe Pass和Adobe访问权限 {#adobe-pass-and-adobe-access}

ADOBE PASS ( [](https://www.adobe.com/products/adobepass/))跨多个内容提供商提供用户/设备身份验证和授权。 用户必须拥有有效的有线电视或卫星电视订阅。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass可以与Adobe访问一起使用来保护媒体内容。 在此方案中，视频播放器(SWF)可以加载另一个名为的SWF， *访问启用码*，由Adobe Systems托管。 此 *访问启用码* 用于连接到Adobe Pass服务，并促进SAML SSO与MVPD的（多频道视频节目分发服务器）身份提供程序的集成。 这包括将用户的浏览器短暂重定向到MVPD登录页面，然后保留AuthN令牌，最后使用缓存的AuthN会话返回到内容网站。

此 *访问启用码* 然后可以促进Adobe Pass服务和MVPD之间的后端授权。 MVPD维护业务逻辑并确定用户有权访问的内容。 该权利将保留在该内容资源的附加AuthZ令牌中，并发送回客户端。

身份验证和授权令牌使用Adobe访问客户端的唯一ID和私钥签名，以避免篡改或欺骗。 此令牌只能通过 *访问启用码*.

视频播放器可以通过调用来触发该过程。 `getAuthorization` 在 *访问启用码*. 当存在有效的AuthN/AuthZ令牌时， *AccessEnabler* 发出对视频播放器的回调，该回调将包含用于播放视频内容的短期媒体令牌。

Adobe Pass提供了一个可以部署到服务器的媒体令牌验证器Java库。 使用Flass Access Server进行内容保护时，您可以将媒体令牌验证器与Adobe访问服务器端插件集成，以便在成功验证媒体令牌后自动颁发通用许可证。 然后，内容会从CDN服务器流式传输到客户端。 为了获取内容许可证，可将短期媒体令牌提交到Adobe访问服务器，在服务器处验证令牌的有效性并且可颁发许可证。

长期AuthN令牌通常由 *访问启用码* 以表示该MVPD订阅者的AuthN。 此外，Adobe Access Server和令牌验证器可由CDN或服务提供商代表内容提供商运行。
