---
description: 当TVSDK在广告服务器响应中遇到损坏的VMAP时，它会调度1109 (NETWORK_AD_URL_FAILED)错误。
keywords: 1109；NETWORK_AD_URL_FAILED；VMAP损坏
title: 断开VMAP的客户端错误处理
exl-id: 268307a9-b72e-45fa-84f2-a8e7d969e2ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 断开VMAP的客户端错误处理 {#client-error-handling-for-broken-vmap}

当TVSDK在广告服务器响应中遇到损坏的VMAP时，它会调度1109 (NETWORK_AD_URL_FAILED)错误。

根据广告服务器响应的性质和广告加载设置，当TVSDK在广告服务器响应中遇到损坏的VMAP时，播放器可能会收到不同的1109错误数。

让我们考虑广告服务器响应指向VMAP XML的情况。 我们还假设广告服务器响应有四个可用的广告插槽，每个插槽都指向相同的VMAP。 最后，假设此VMAP已损坏。

在此方案中，如果启用了延迟广告解析( [启用延迟广告解析](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md))，TVSDK将调度两个1109错误（而不是预期的）：在时间轴上的每个解析传递上都调度一个错误。 这是因为启用延迟广告解析后，TVSDK将分两阶段解析广告：第一阶段发生在前置广告的内容播放开始之前，第二阶段发生在播放开始之后，适用于中置广告和后置广告。

>[!NOTE]
>
>在此场景中，如果您禁用延迟广告解析，TVSDK将仅触发一个1109错误（仅有一个解析传递）。
