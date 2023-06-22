---
title: 疑难解答和调试
description: 疑难解答和调试
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 疑难解答和调试 {#troubleshooting-debugging}

PrimetimeAd Insertion提供了用于识别和诊断视频交付所有阶段中可能发生的问题的工具，例如CDN交付错误、广告创意错误或客户端连接错误。

PrimetimeAd Insertion支持通过 [API参数Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` 或 `ptdebug=AdCall` 到引导URL。 日志将输出到HTTP响应标头和PrimetimeAd Insertion控制台。 此参数仅用于本地化测试，不适用于生产流。 有关启用详细日志记录时消息类型的详细信息，请参阅 [ptdebug记录详细日志中的事件](verbose-logging.md#ptdebug-logging-events).

PrimetimeAd Insertion还可以通过X-ADBE-AI-X1标头针对所有请求进行性能调试，该标头可用于测量任何给定请求上的性能和广告插入。 无论是否启用详细日志记录，此请求标头均可用。 有关更多信息，请参阅 [详细标头：X-ADBE-PTAI-X1](debugging-headers.md).
