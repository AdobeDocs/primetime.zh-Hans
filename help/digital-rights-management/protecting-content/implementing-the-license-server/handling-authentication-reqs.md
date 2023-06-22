---
title: 处理身份验证请求
description: 处理身份验证请求
copied-description: true
exl-id: 64d23db0-254d-46b1-8317-ba0381509b44
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 处理身份验证请求 {#handle-authentication-requests}

此 `AuthenticationHandler` 类用于处理身份验证请求。 它仅用于用户名/密码身份验证。

在生成身份验证令牌时，必须指定令牌过期日期。 自定义属性也可以包含在令牌中。 如果设置，则在后续请求中发送身份验证令牌时，服务器将看到这些属性。 参见 [处理许可证请求](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) 以了解有关处理自定义身份验证令牌的信息。

该处理程序读取身份验证请求并解析请求消息，当时 `parseRequest()` 称为。 服务器实施会检查请求中的用户凭据，如果凭据有效，则生成 `AuthenticationToken` 对象（通过调用） `getRequest().generateAuthToken()`. 如果 `AuthenticationRequestMessage.generateAuthToken()` 之前未调用 `close()`，则会发送身份验证失败错误代码。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“元数据中的许可证服务器URL： + ” [!DNL /flashaccess/authn/v4]“。 如果协议版本3是客户端或服务器支持的最大版本，则Adobe Primetime DRM客户端将身份验证请求发送到“元数据中的许可证服务器URL”+ [!DNL /flashaccess/authn/v3]“。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/authn/v1]”
