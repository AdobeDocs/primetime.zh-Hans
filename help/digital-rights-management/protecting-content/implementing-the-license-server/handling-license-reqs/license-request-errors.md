---
title: 许可证请求错误处理
description: 许可证请求错误处理
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 许可证请求错误处理 {#license-request-error-handling}

如果在请求解析期间出错，则 `HandlerParsingException` 发生。 此异常包括返回到客户端的错误信息。 如果需要检索错误信息，则需要调用 `HandlerParsingException.getErrorData()`. 如果由于DRM策略要求未得到满足而在许可证的生成过程中发生错误， `PolicyEvaluationException` 发生。 此例外情况还包括 `ErrorData` 返回给客户端。

请参阅API文档，了解 `LicenseRequestMessage.generateLicense()` 有关如何在许可证生成期间评估DRM策略的详细信息。
