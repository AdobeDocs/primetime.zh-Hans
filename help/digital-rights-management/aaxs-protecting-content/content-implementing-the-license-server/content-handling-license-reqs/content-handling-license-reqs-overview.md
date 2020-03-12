---
seo-title: 概述
title: 概述
uuid: d3bfa65b-2360-4843-b59e-71451fa62a2c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 概述{#overview}

要请求许可证，客户端会发送在打包过程中嵌入到内容中的元数据。 许可证服务器使用内容元数据中的信息生成许可证。

将读 `LicenseHandler` 取许可证请求并解析该请求。 `LicenseHandler`扩展 `BatchHandlerBase` 以适应批量许可证请求，但Adobe Access客户端当前不支持此功能。 该方 `getRequests()` 法将返回对象列 `LicenseRequestMessage` 表。 调用者应遍历该请求 `LicenseRequestMessages`，并且对于每个请求，应生成许可证或设置错误代码(有关详细信息，请参阅 `LicenseRequestMessage` API参考文档)。 对于每个许可证请求，服务器确定它是否将发出许可证。 调 `LicenseRequestMessage.getContentInfo()` 用以获取从内容元数据中提取的信息，包括内容ID、许可证ID和策略。

* 请求处理函数类为 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为元数据中的“许可证服务器URL”:+ &quot;/flashaccess/license/v4&quot;。 如果客户端或服务器支持的协议版本3是最大版本，则Adobe Access客户端将向“元数据中的许可证服务器URL”+“/flashaccess/license/v3”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“/flashaccess/license/v1”

如果解析请求时出错，则会引 `HandlerParsingException` 发一个错误。 此异常包含要返回给客户端的错误信息。 要检索错误信息，请调用 `HandlerParsingException.getErrorData()`。 如果由于未满足策略要求而生成许可证时出错，则会引 `PolicyEvaluationException` 发错误。 此例外还包括 `ErrorData` 要返回到客户端的例外。 有关在生成许可证时如 `LicenseRequestMessage.generateLicense()` 何评估策略的详细信息，请参阅API文档。

许可证和错误在调用时同 `LicenseHandler.close()` 时发送。

设备可能具有同一内容的多个许可证（同一许可证ID），但特定许可证ID和策略ID只能有一个许可证。 如果收到的许可证具有重复的LicenseID/PolicyID，则新许可证将替换旧许可证，但前提是新许可证的发布日期晚于现有许可证的发布日期。 此逻辑用于处理嵌入到内容中的许可证，因此，建议不要在内容块中嵌入多个具有相同策略ID的许可证。 同样的逻辑适用于通过 `DRMManager.storeVoucher()` ActionScript3 API传递给客户端的许可证；如果客户端已经拥有稍后发布日期的许可证，则可能会忽略提供的许可证。
