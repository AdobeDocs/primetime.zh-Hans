---
title: 应用广告分辨率约束
description: 应用广告分辨率约束
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 应用广告分辨率约束 {#apply-ad-resolution-constraints}

在某些情况下，特定广告提供商响应缓慢，这可能会导致视频启动时间增加。 PrimetimeAd Insertion支持广告请求超时和整个广告解析阶段，以限制这些慢速广告提供商的影响。  如果下游广告提供商响应速度太慢，也可以插入后备广告。  有关更多信息，请参阅 [`ptadtimeout` BootstrapAPI中的参数](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
