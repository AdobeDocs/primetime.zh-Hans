---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 概述{#overview}

要请求许可证，客户端会发送在打包过程中嵌入到内容中的元数据。 许可证服务器使用内容元数据中的信息生成许可证。

`LicenseHandler`读取许可证请求并解析该请求。 `LicenseHandler`扩展 `BatchHandlerBase` 以容纳批许可证请求，尽管Adobe Access客户端当前不支持此功能。`getRequests()`方法将返回`LicenseRequestMessage`对象的列表。 调用方应遍历`LicenseRequestMessages`，对于每个请求，生成许可证或设置错误代码（有关详细信息，请参阅`LicenseRequestMessage` API参考文档）。 对于每个许可证请求，服务器确定它是否将颁发许可证。 调用`LicenseRequestMessage.getContentInfo()`以获取从内容元数据（包括内容ID、许可证ID和策略）中提取的信息。

* 请求处理程序类为`com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为“元数据中的许可证服务器URL:+ &quot;/flashaccess/license/v4&quot;。 如果客户端或服务器支持的协议版本3是最大版本，Adobe Access客户端将向“元数据中的许可证服务器URL”+“/flashaccess/license/v3”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“/flashaccess/license/v1”

如果解析请求时出错，则引发`HandlerParsingException`。 此异常包含要返回给客户端的错误信息。 要检索错误信息，请调用`HandlerParsingException.getErrorData()`。 如果由于未满足策略要求而生成许可证时出错，则会引发`PolicyEvaluationException`。 此异常还包括要返回到客户端的`ErrorData`。 有关在生成许可证期间如何评估策略的详细信息，请参阅`LicenseRequestMessage.generateLicense()`的API文档。

在调用`LicenseHandler.close()`时，许可证和错误会同时发送。

设备可能具有同一内容的多个许可证（同一许可证ID），但只能具有特定许可证ID和策略ID的一个许可证。 如果它收到具有重复许可证ID/策略ID的许可证，则只有新许可证的发布日期晚于现有许可证的发布日期，新许可证才会替换旧许可证。 此逻辑用于处理嵌入到内容中的许可证，因此，建议不要在内容块中嵌入多个具有相同策略ID的许可证。 同样的逻辑适用于通过`DRMManager.storeVoucher()` ActionScript3 API传递给客户端的许可证；如果客户端已经拥有一个许可证，并且该许可证的发布日期在以后，则可能会忽略提供的许可证。
