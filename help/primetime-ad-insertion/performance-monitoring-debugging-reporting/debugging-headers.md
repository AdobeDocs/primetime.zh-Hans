---
title: 调试标头
description: null
translation-type: tm+mt
source-git-commit: 45e5c8e6144adf4a405bde7d8d19505b7ad549e0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 7%

---


# 调试标头(X-ADBE-AI-X1){#debugging-headers}

SSAI发送HTTP头，这些头可用于收集信息并确定生产会话的性能，该会话位于X-ADBE-AI-X1头中。

标题示例：
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

字段的说明如下：

| 名称 | 说明 | 示例 |
|--- |--- |--- |
| isActivePreroll | 是否发送了预先广告呼叫 | 0 |
| isActiveMidroll | 是否已发送广告呼叫Midroll-roll | 3 |
| 请求ID | 内部SSAI | 1594181097704 |
| 会话ID | 请求的会话ID | 15126333-5ba9-49b8-a219-4f37e60d259c |
| 流类型 | u=variant, l=live, v=vod | v |
| isBootstrap | 此请求是否为引导调用 | 0 |
| 广告中断数 | 此清单中的广告分时段总数 | 1 |
| 广告中断总持续时间 | 广告中断的总持续时间，以秒为单位 | 30 |
| 广告呼叫数 | 此请求中发送的广告调用数 | 2 |
| 重定向广告呼叫数 | 此请求中发送的重定向广告调用数 | 3 |
| 广告呼叫总持续时间 | 广告呼叫总处理时间 | 199 |
| 插入的广告计数 | 插入到清单中的广告数 | 2 |
| 源清单请求时间 | 仅提取内容所花费的时间 | 185 |
| 请求总时间 | 获取内容和广告所花费的总时间 | 497 |
| 广告清单提取时间（总计） | 获取广告清单的总时间 | 204 |
| 广告清单提取时间（实际） | 并行获取广告清单的实际时间量 | 104 |
| 内容缓存点击 | 内容缓存点击数 | 0 |
| 内容缓存未命中 | 内容缓存未命中数 | 1 |
| 广告清单缓存命中 | 广告清单缓存点击数 | 0 |
| 广告清单缓存未命中 | 广告清单高速缓存未命中数 | 4 |