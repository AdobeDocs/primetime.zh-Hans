---
title: 概述
description: 概述
copied-description: true
exl-id: f1a55d5c-c7df-4b8f-8c1e-875d30026069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概述{#overview}

要请求许可证，客户端会在打包期间发送嵌入到内容中的元数据。 许可证服务器使用内容元数据中的信息来生成许可证。

此 `LicenseHandler` 读取许可证请求并解析该请求。 `LicenseHandler`扩展 `BatchHandlerBase` 以容纳批量许可证请求，但Adobe访问客户端当前不支持此功能。 此 `getRequests()` 方法将返回以下列表： `LicenseRequestMessage` 对象。 调用方应通过 `LicenseRequestMessages`，并为每个请求生成许可证或设置错误代码(请参阅 `LicenseRequestMessage` API参考文档（了解详细信息）。 对于每个许可证请求，服务器确定它是否将颁发许可证。 调用 `LicenseRequestMessage.getContentInfo()` 获取从内容元数据提取的信息，包括内容ID、许可证ID和策略。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“License Server URL in metadata： + &quot;/flashaccess/license/v4&quot;。 如果协议版本3是客户端或服务器支持的最大版本，则Adobe访问客户端将向“License Server URL in metadata”+ &quot;/flashaccess/license/v3&quot;发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“/flashaccess/license/v1”

如果解析请求时出错，则 `HandlerParsingException` 被抛出。 此异常包含要返回到客户端的错误信息。 要检索错误信息，请调用 `HandlerParsingException.getErrorData()`. 如果由于策略要求未得到满足而在生成许可证时发生错误， `PolicyEvaluationException` 被抛出。 此例外情况还包括 `ErrorData` 返回给客户端。 请参阅API文档，了解 `LicenseRequestMessage.generateLicense()` 以获取有关如何在许可证生成期间评估策略的详细信息。

许可证和错误会同时发送，当 `LicenseHandler.close()` 称为。

一个设备可能具有多个用于相同内容（相同许可证ID）的许可证，但特定许可证ID和策略ID只能有一个许可证。 如果收到具有重复LicenseID/PolicyID的许可证，则只有在新许可证的颁发日期晚于现有许可证的颁发日期时，新许可证才会替换旧许可证。 此逻辑用于处理嵌入到内容中的许可证，因此，建议不要在一个内容块中嵌入多个具有同一策略ID的许可证。 相同的逻辑适用于通过 `DRMManager.storeVoucher()` ActionScript3 API；如果客户端已拥有许可证，且许可证的颁发日期较晚，则可以忽略所提供的许可证。
