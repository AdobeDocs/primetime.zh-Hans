---
seo-title: 处理身份验证请求
title: 处理身份验证请求
uuid: abcb9cf6-668e-405c-9659-9ed1bcc33024
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 处理身份验证请求{#handle-authentication-requests}

`AuthenticationHandler`类用于处理身份验证请求。 它仅用于用户名／密码身份验证。

在生成身份验证令牌时，必须指定令牌到期日期。 自定义属性也可能包含在令牌中。 如果设置，则当在后续请求中发送身份验证令牌时，服务器将看到这些属性。 有关处理自定义身份验证令牌的信息，请参阅[处理许可证请求](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md)。

处理函数读取身份验证请求，并在调用`parseRequest()`时解析请求消息。 服务器实现检查请求中的用户凭据，如果凭据有效，则通过调用`getRequest().generateAuthToken()`来生成`AuthenticationToken`对象。 如果在`close()`之前未调用`AuthenticationRequestMessage.generateAuthToken()`，则会发送身份验证失败错误代码。

* 请求处理函数类为`com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为元数据中的“许可证服务器URL:+ &quot; [!DNL /flashaccess/authn/v4]&quot;。 如果协议版本3是客户端或服务器支持的最大版本，则Adobe PrimetimeDRM客户端会向“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/authn/v3]”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/authn/v1]”

