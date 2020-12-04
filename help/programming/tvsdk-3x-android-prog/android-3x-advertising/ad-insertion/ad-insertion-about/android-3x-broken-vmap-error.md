---
description: 当TVSDK在广告服务器响应中遇到中断的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: 当TVSDK在广告服务器响应中遇到中断的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。
seo-title: 中断的VMAP的客户端错误处理
title: 中断的VMAP的客户端错误处理
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 对断开的VMAP {#client-error-handling-for-broken-vmap}的客户端错误处理

当TVSDK在广告服务器响应中遇到中断的VMAP时，它将调度1109(NETWORK_AD_URL_FAILED)错误。

根据广告服务器响应的性质和广告加载设置，当TVSDK在广告服务器响应中遇到中断的VMAP时，播放器可能会收到不同的1109个错误。

让我们考虑广告服务器响应指向VMAP XML的情况。 假设广告服务器响应有四个可用广告插槽，每个插槽指向同一VMAP。 最后，假设此VMAP已损坏。

在此方案中，如果启用延迟广告解析（[启用延迟广告解析](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)）,TVSDK将调度两个1109错误（不是预期的错误）:每次解析传递通过时间线时都会调度一个错误。 这是因为启用延迟广告解析时，TVSDK会以2次方式解析广告：第一次传递发生在前置广告的内容播放开始之前，第二次传递发生在中置广告和后置广告的播放开始之后。

>[!NOTE]
>
>在此方案中，如果禁用延迟广告解析，TVSDK将仅触发一个1109错误（仅一个解析通过）。