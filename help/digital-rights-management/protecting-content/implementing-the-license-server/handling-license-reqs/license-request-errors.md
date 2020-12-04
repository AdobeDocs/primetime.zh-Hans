---
seo-title: 许可证请求错误处理
title: 许可证请求错误处理
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 许可证请求错误处理{#license-request-error-handling}

如果在请求解析过程中发生错误，则出现`HandlerParsingException`。 此异常包括返回给客户端的错误信息。 如果需要检索错误信息，则需要调用`HandlerParsingException.getErrorData()`。 如果由于未满足DRM策略要求而在生成许可证期间发生错误，则出现`PolicyEvaluationException`。 此异常还包括要返回到客户端的`ErrorData`。

有关在生成许可证期间如何评估DRM策略的详细信息，请参阅`LicenseRequestMessage.generateLicense()`的API文档。
