---
seo-title: Adobe Pass和Adobe Access
title: Adobe Pass和Adobe Access
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adobe Pass和Adobe Access {#adobe-pass-and-adobe-access}

Adobe Pass( [](https://www.adobe.com/products/adobepass/))提供跨多个内容提供商的用户／设备身份验证和授权。 用户必须有有效的有线电视或卫星电视订阅。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass可与Adobe Access一起使用，以保护媒体内容。 在此方案中，视频播放器(SWF)可以加载另一个称为 *Access Enabler*（由Adobe Systems托管）的SWF。 Access *Enabler* （访问启用程序）用于连接到Adobe Pass服务，并促进SAML SSO与MVPD（多通道视频编程分销商）标识提供者系统的集成。 这包括将用户的浏览器短暂重定向到MVPD登录页面，然后使AuthN令牌保持不变，最后返回到具有缓存的AuthN会话的内容网站。

然后， *Access Enabler* （访问启用程序）便于在Adobe Pass服务和MVPD之间进行后端授权。 MVPD维护业务逻辑并确定用户有权访问哪些内容。 该授权将保留在该内容资源的其他AuthZ令牌中，并发送回客户端。

身份验证和授权令牌使用Adobe Access客户端的唯一ID和私钥进行签名，以避免篡改或欺骗。 此令牌只能通过访问启用 *码访问*。

视频播放器可以通过调用访问启用程序 `getAuthorization` 来触发 *该过程*。 当有效的AuthN/AuthZ令牌存在时， *AccessEnabler* 会向视频播放器发出回调，该视频播放器将包含用于播放视频内容的短期媒体令牌。

Adobe Pass提供可部署到服务器的媒体令牌验证程序Java库。 当使用Flash Access服务器进行内容保护时，您可以将媒体令牌验证程序与Adobe Access服务器端插件集成，以在成功验证媒体令牌后自动发布通用许可证。 然后，内容从CDN服务器流式传输到客户端。 要获取内容许可证，可将短期媒体令牌提交到Adobe Access服务器，其中验证令牌的有效性并发放许可证。

长期使用的AuthN令牌通常由所有内容开发者的 *Access Enabler* 使用，以代表该MVPD订阅者的AuthN。 此外，Adobe Access Server和令牌验证器可由CDN或代表内容提供商的服务提供商操作。
