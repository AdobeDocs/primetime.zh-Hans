---
seo-title: 处理身份验证请求
title: 处理身份验证请求
uuid: 036582d4-611c-4772-b247-81a3144fd5d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 处理身份验证请求{#handling-authentication-requests}

类 `AuthenticationHandler` 用于处理身份验证请求。 它仅用于用户名／密码身份验证。

在生成身份验证令牌时，必须指定令牌的到期日期。 自定义属性也可能包含在令牌中。 如果设置了此类属性，则当在后续请求中发送身份验证令牌时，这些属性对服务器可见。 有关处 [理自定义身份验证令牌的信息](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) ，请参阅处理许可证请求。

该处理函数读取一个身份验证请求，并在调用时分析该 `parseRequest()` 请求消息。 服务器实现检查请求中的用户凭据，如果凭据有效，则通过调用 `AuthenticationToken` 生成对象 `getRequest().generateAuthToken()`。 如果 `AuthenticationRequestMessage.generateAuthToken()` 之前未调用， `close()`则会发送身份验证失败错误代码。

* 请求处理函数类为 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为元数据中的“许可证服务器URL”:+ &quot;/flashaccess/authn/v4&quot;。 如果客户端或服务器支持的协议版本3是最大版本，则Adobe Access客户端将向“元数据中的许可证服务器URL”+“/flashaccess/authn/v3”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“/flashaccess/authn/v1”

