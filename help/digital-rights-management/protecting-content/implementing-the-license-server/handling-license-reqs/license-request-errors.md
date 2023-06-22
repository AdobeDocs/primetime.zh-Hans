---
title: 许可证请求错误处理
description: 许可证请求错误处理
copied-description: true
exl-id: 7cfdebc5-db2b-4629-98e6-31ad71cb424c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 许可证请求错误处理 {#license-request-error-handling}

如果在请求解析过程中出现错误，则 `HandlerParsingException` 发生。 此异常包括返回到客户端的错误信息。 如果需要检索错误信息，则需要调用 `HandlerParsingException.getErrorData()`. 如果在生成许可证期间由于DRM策略要求未得到满足而发生错误， `PolicyEvaluationException` 发生。 此例外情况还包括 `ErrorData` 返回给客户端。

请参阅API文档，了解 `LicenseRequestMessage.generateLicense()` 有关如何在许可证生成期间评估DRM策略的详细信息。
