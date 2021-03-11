---
description: 当TVSDK在广告服务器响应中遇到损坏的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。
keywords: 1109;NETWORK_AD_URL_FAILED；断开的VMAP
title: 对损坏的VMAP的客户端错误处理
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 对损坏的VMAP {#client-error-handling-for-broken-vmap}的客户端错误处理

当TVSDK在广告服务器响应中遇到损坏的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。

根据广告服务器响应的性质以及广告加载设置，当TVSDK在广告服务器响应中遇到损坏的VMAP时，您的播放器可能会收到不同的1109个错误。

让我们考虑广告服务器响应指向VMAP XML的情况。 假设广告服务器响应有四个可用广告插槽，每个插槽指向同一VMAP。 最后，假设此VMAP已损坏。

在此方案中，如果启用了延迟广告解析（[启用延迟广告解析](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md)），TVSDK将调度两个1109错误（不是预期的错误）：在时间线上的每个分析传递上调度一个错误。 这是因为，启用延迟广告解析时，TVSDK会以2次方式解析广告：第一遍发生在前置广告的内容播放开始之前，第二遍发生在中间和后置广告的播放开始之后。

>[!NOTE]
>
>在此方案中，如果禁用延迟广告解析，TVSDK将仅触发一个1109错误（仅一次分析通过）。

