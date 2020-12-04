---
seo-title: 处理域取消注册请求
title: 处理域取消注册请求
uuid: 6f056b2b-374d-4e4d-926a-68605b2c923b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 处理域取消注册请求{#handling-domain-de-registration-requests}

如果客户端应用程序需要离开域，它将调用`DRMManager.removeFromDeviceGroup()`ActionScriptAPI或`leaveLicenseDomain()` iOS API来启动域取消注册过程。 域取消注册是一个两阶段的过程。 客户端首先发送取消注册预览请求。 域服务器检查请求并确定是否允许客户端离开域（如果计算机当前不是域的一部分，则可能返回错误）。 在成功响应后，客户端将删除其域凭据和颁发给该域的任何许可证，然后发送取消注册请求。

* 请求处理函数类为`com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为元数据中的“域服务器URL:+ &quot;/flashaccess/dereg/v4&quot;。 否则，请求URL为元数据&quot; + &quot;/flashaccess/dereg/v3&quot;中的域服务器URL

在处理域取消注册请求时，服务器使用`getRequestPhase()`确定客户端是处于预览还是取消注册阶段。 在预览阶段，域服务器检查请求并确定是否允许客户端离开域（例如，如果计算机当前不是域的一部分，则可以拒绝该请求）。 在取消注册阶段，服务器记录计算机已离开域的事实。 强烈建议服务器评估预览请求中与实际取消注册请求中相同的逻辑，以最大限度地降低第二阶段失败的可能性。
