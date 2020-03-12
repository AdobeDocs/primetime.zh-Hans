---
description: 当TVSDK在广告服务器响应中遇到损坏的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: 当TVSDK在广告服务器响应中遇到损坏的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。
seo-title: 针对损坏的VMAP的客户端错误处理
title: 针对损坏的VMAP的客户端错误处理
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 针对损坏的VMAP的客户端错误处理 {#client-error-handling-for-broken-vmap}

当TVSDK在广告服务器响应中遇到损坏的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。

根据广告服务器响应的性质和广告加载设置，当TVSDK在广告服务器响应中遇到损坏的VMAP时，您的播放器可能会收到不同数目的1109错误。

让我们考虑广告服务器响应指向VMAP XML的场景。 假设广告服务器响应有四个可用广告插槽，每个插槽指向同一VMAP。 最后，假设这个VMAP被破坏。

在此方案中，如果启用了延迟广告解析([Enable lazy ad resolving](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)),TVSDK将调度两个1109错误（不是预期的错误）:在时间线上的每个解析传递中都会调度一个错误。 这是因为，当启用延迟广告解析时，TVSDK会以2次方式解析广告：对于中间广告和后置广告，第一遍是在内容开始播放之前进行的，第二遍是在播放开始之后进行的。

>[!NOTE]
>
>在此方案中，如果禁用延迟广告解析，TVSDK将仅触发一个1109错误（仅一次解析通过）。