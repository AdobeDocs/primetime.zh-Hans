---
title: 概述
description: 概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概述{#overview}

为了请求许可证，客户端在打包期间发送嵌入到内容中的元数据。 许可证服务器使用内容元数据中的信息来生成许可证。

此 `LicenseHandler` 读取许可证请求并解析该请求。 `LicenseHandler`扩展 `BatchHandlerBase` 以容纳批量许可证请求，但Adobe访问客户端当前不支持此功能。 此 `getRequests()` 方法将返回 `LicenseRequestMessage` 对象。 调用方应通过 `LicenseRequestMessages`，并为每个请求生成许可证或设置错误代码(请参阅 `LicenseRequestMessage` API参考文档（以了解详细信息）。 对于每个许可证请求，服务器将确定是否颁发许可证。 调用 `LicenseRequestMessage.getContentInfo()` 获取从内容元数据提取的信息，包括内容ID、许可ID和策略。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“元数据： + &quot;/flashaccess/license/v4中的许可证服务器URL”。 如果协议版本3是客户端或服务器支持的最大版本，则Adobe访问客户端将向“License Server URL in metadata”+“/flashaccess/license/v3”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“/flashaccess/license/v1”

如果解析请求时出错，则 `HandlerParsingException` 被抛出。 此异常包含要返回到客户端的错误信息。 要检索错误信息，请调用 `HandlerParsingException.getErrorData()`. 如果由于未满足策略要求而导致在生成许可证时出错， `PolicyEvaluationException` 被抛出。 此例外情况还包括 `ErrorData` 返回给客户端。 请参阅API文档，了解 `LicenseRequestMessage.generateLicense()` 以获取有关如何在许可证生成期间评估策略的详细信息。

许可证和错误在下列情况下同时发送： `LicenseHandler.close()` 称为。

一个设备可能具有多个用于相同内容的许可证（相同的许可证ID），但只能有一个用于特定许可证ID和策略ID的许可证。 如果收到具有重复LicenseID/PolicyID的许可证，则只有在新许可证的颁发日期晚于现有许可证的颁发日期时，新许可证才会替换旧许可证。 此逻辑用于处理嵌入到内容中的许可证，因此，建议不要在一个内容块中嵌入多个具有同一策略ID的许可证。 相同的逻辑适用于通过 `DRMManager.storeVoucher()` ActionScript3 API；如果客户端已拥有许可证，并且许可证的发布日期较晚，则提供的许可证可能会被忽略。
