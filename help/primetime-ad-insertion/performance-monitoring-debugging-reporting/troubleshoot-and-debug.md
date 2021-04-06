---
title: 疑难解答和调试
description: 疑难解答和调试
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# {#troubleshooting-debugging}疑难解答和调试

PrimetimeAd Insertion优惠工具可用于识别和诊断视频投放所有阶段可能发生的问题，如CDN投放错误、创意错误或客户端连接错误。

PrimetimeAd Insertion支持通过引导URL的[BootstrapAPI参数](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true`或`ptdebug=AdCall`进行详细记录。 日志将输出到HTTP响应头和PrimetimeAd Insertion控制台。 此参数仅用于本地化测试，而不用于生产流。 有关启用详细日志记录时消息类型的详细信息，请参阅详细日志记录](verbose-logging.md#ptdebug-logging-events)中的[ptdebug日志记录事件。

PrimetimeAd Insertion还使用X-ADBE-AI-X1头提供所有请求的性能调试，该头可用于评估任何给定请求的性能和广告插入情况。 无论是否启用详细日志记录，此请求标头都可用。 有关详细信息，请参阅[详细标题：X-ADBE-PTAI-X1](debugging-headers.md)。
