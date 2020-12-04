---
seo-title: Adobe Primetime身份验证和Adobe PrimetimeDRM
title: Adobe Primetime身份验证和Adobe PrimetimeDRM
uuid: 44fe3956-efb5-4fc5-97e2-37abb6554322
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Adobe Primetime身份验证和Adobe PrimetimeDRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

Adobe Primetime身份验证([https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/))提供跨多个内容提供商的用户／设备身份验证和授权。 用户必须具有有效的有线电视或卫星电视订阅。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Primetime身份验证可以与AdobePrimetime DRM一起使用，以保护媒体内容。 在这种情况下，视频播放器(SWF)可以加载另一个SWF，称为&#x200B;*访问启用码*，由Adobe Systems托管。 *访问启用程序*&#x200B;用于连接到Adobe Primetime身份验证服务，并促进SAML SSO与MVPD（多通道视频编程分发商）标识提供者系统的集成。 这包括将用户的浏览器短暂重定向到MVPD登录页，然后保持AuthN令牌，最后返回到具有缓存的AuthN会话的内容网站。

然后，*访问启用程序*&#x200B;便于在Adobe Primetime身份验证服务和MVPD之间进行后端授权。 MVPD维护业务逻辑并确定用户有权访问哪些内容。 该授权将保留在该内容资源的附加AuthZ令牌中，并发送回客户端。

验证和授权令牌使用Primetime DRM客户端的唯一ID和私钥进行签名，以避免篡改或欺骗。 此令牌只能通过&#x200B;*访问启用码*&#x200B;访问。

视频播放器可以通过调用&#x200B;*访问启用码*&#x200B;上的`getAuthorization`来触发该过程。 当存在有效的AuthN/AuthZ令牌时，*AccessEnabler*&#x200B;将向视频播放器发出回调，该视频播放器将包含用于播放视频内容的短时媒体令牌。

Adobe Primetime身份验证提供可部署到服务器的媒体令牌validator Java库。 当使用Primetime DRM服务器进行内容保护时，您可以将媒体令牌验证器与Primetime DRM服务器端插件集成，以在成功验证媒体令牌后自动发布通用许可证。 然后，内容会从CDN服务器流式传输到客户端。 为了获得内容许可，可向Primetime DRM服务器提交短时媒体令牌，其中验证令牌的有效性并可发放许可。

*访问启用码*&#x200B;在所有内容开发者中通常使用长寿命的AuthN令牌来代表该MVPD订阅者的AuthN。 此外，Primetime DRM服务器和令牌验证器可由CDN或服务提供商代表内容提供商运行。