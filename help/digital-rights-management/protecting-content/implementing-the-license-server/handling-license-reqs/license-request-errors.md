---
title: 许可证请求错误处理
description: 许可证请求错误处理
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 处理{#license-request-error-handling}的许可证请求错误

如果在请求解析期间发生错误，则发生`HandlerParsingException`。 此异常包括返回给客户端的错误信息。 如果需要检索错误信息，则需要调用`HandlerParsingException.getErrorData()`。 如果由于未满足DRM策略要求而在生成许可证期间发生错误，则发生`PolicyEvaluationException`。 此异常还包括要返回到客户端的`ErrorData`。

有关在生成许可证时如何评估DRM策略的详细信息，请参阅`LicenseRequestMessage.generateLicense()`的API文档。
