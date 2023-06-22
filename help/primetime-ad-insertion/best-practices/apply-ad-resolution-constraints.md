---
title: 应用广告分辨率限制
description: 应用广告分辨率限制
copied-description: true
exl-id: aae17be8-d23c-4c5c-90fd-7ee6fba69e9a
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 应用广告分辨率限制 {#apply-ad-resolution-constraints}

在某些情况下，特定广告提供商响应缓慢，这可能会导致视频启动时间增加。 PrimetimeAd Insertion支持广告请求超时和整个广告解析阶段，以限制这些慢速广告提供商的影响。  如果下游广告提供商响应速度太慢，也可以插入后备广告。  有关更多信息，请参阅 [`ptadtimeout` BootstrapAPI中的参数](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
