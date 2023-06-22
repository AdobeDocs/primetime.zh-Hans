---
title: 处理域取消注册请求
description: 处理域取消注册请求
copied-description: true
exl-id: f29507b5-d32a-4b22-a02e-6701b86db133
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 处理域取消注册请求{#handling-domain-de-registration-requests}

如果客户端应用程序需要离开域，它将调用 `DRMManager.removeFromDeviceGroup()`ActionScriptAPI或 `leaveLicenseDomain()` iOS API可启动域注销流程。 域注销是一个两阶段的过程。 客户端首先发送注销预览请求。 域服务器检查请求并确定是否允许客户端离开域（如果计算机当前不是域的一部分，可能会返回错误）。 成功响应后，客户端将删除其域凭据和颁发给该域的任何许可证，然后发送注销请求。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“元数据： + &quot;/flashaccess/dereg/v4中的域服务器URL”。 否则，请求URL是元数据“ + &quot;/flashaccess/dereg/v3”中的域服务器URL

处理域注销请求时，服务器使用 `getRequestPhase()` 以确定客户端是处于预览阶段还是取消注册阶段。 在预览阶段，域服务器检查请求并确定是否允许客户端离开域（例如，如果计算机当前不是域的一部分，请求可能会被拒绝）。 在注销阶段，服务器记录计算机已离开域的事实。 强烈建议服务器评估预览请求中与实际注销请求中相同的逻辑，以最大程度地减少第二阶段失败的可能性。
