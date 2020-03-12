---
seo-title: 许可证请求错误处理
title: 许可证请求错误处理
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证请求错误处理 {#license-request-error-handling}

如果在请求解析过程中出现错误，则会发 `HandlerParsingException` 生。 此异常包括返回给客户端的错误信息。 如果您需要检索错误信息，您需要调用 `HandlerParsingException.getErrorData()`。 如果由于未满足DRM策略要求而在生成许可证期间发生错误，则会发 `PolicyEvaluationException` 生。 此例外还包括 `ErrorData` 要返回到客户端的例外。

有关在生成许可证 `LicenseRequestMessage.generateLicense()` 期间如何评估DRM策略的详细信息，请参阅API文档。
