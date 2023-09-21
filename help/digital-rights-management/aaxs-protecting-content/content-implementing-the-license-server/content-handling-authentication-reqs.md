---
title: 处理身份验证请求
description: 处理身份验证请求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 处理身份验证请求{#handling-authentication-requests}

此 `AuthenticationHandler` 类用于处理身份验证请求。 它仅用于用户名/密码身份验证。

在生成身份验证令牌时，必须指定令牌过期日期。 令牌中还可包含自定义属性。 如果设置，则在后续请求中发送身份验证令牌时，服务器将看到这些属性。 请参阅 [处理许可证请求](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) 以了解有关处理自定义身份验证令牌的信息。

处理程序读取身份验证请求并解析请求消息，当 `parseRequest()` 称为。 服务器实施会检查请求中的用户凭据，如果凭据有效，则生成 `AuthenticationToken` 通过调用对象 `getRequest().generateAuthToken()`. 如果 `AuthenticationRequestMessage.generateAuthToken()` 之前未调用 `close()`，将会发送身份验证失败错误代码。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“License Server URL in metadata： + &quot;/flashaccess/authn/v4”。 如果协议版本3是客户端或服务器支持的最大版本，则Adobe访问客户端将向“License Server URL in metadata”+“/flashaccess/authn/v3”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“/flashaccess/authn/v1”
