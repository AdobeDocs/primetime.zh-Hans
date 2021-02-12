---
title: 疑难解答和调试
description: null
translation-type: tm+mt
source-git-commit: 242b5a2875ebc0e0020296ce9489dd54438b5ad0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 疑难解答和调试{#troubleshooting-debugging}

PrimetimeAd Insertion优惠工具可用于识别和诊断视频投放的所有阶段可能发生的问题，如CDN投放错误、广告创意错误或客户端连接错误。

PrimetimeAd Insertion通过引导URL的[BootstrapAPI参数](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true`或`ptdebug=AdCall`支持详细记录。 日志将输出到HTTP响应头和PrimetimeAd Insertion控制台。 此参数仅用于本地化测试，而不用于生产流。 有关启用详细日志记录时消息类型的详细信息，请参阅详细日志记录中的[ptdebug日志事件](verbose-logging.md#ptdebug-logging-events)。

PrimetimeAd Insertion还使用X-ADBE-AI-X1头提供所有请求的性能调试，该头可用于衡量任何给定请求的性能和广告插入。 无论是否启用详细记录，此请求标头都可用。 有关详细信息，请参阅[详细标题：X-ADBE-PTAI-X1](debugging-headers.md)。
