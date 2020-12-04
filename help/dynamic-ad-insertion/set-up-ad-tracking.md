---
title: 设置广告跟踪
description: 设置广告跟踪
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 设置广告跟踪{#ser-up-ad-tracking}

大多数广告商需要有关广告被浏览的时间、时长以及成功程度的信息。 PrimetimeAd Insertion支持客户端、服务器端和混合广告跟踪，以在收集此信息时提供灵活性。

## 使用VMAP/JSON {#client-side-ad-tracking-vmap-json}进行客户端广告跟踪

在客户端广告跟踪中，服务器向客户端发送JSON、VMAP或清单内结构，该结构指定跟踪事件和URL以及广告拼接播放列表。

要启用客户端广告跟踪，请在[BootstrapAPI](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)中指定以下参数。

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>设置`pttrackingmode=simple`将导致初始引导API请求返回JSON响应，而不是HLS或DASH文档。

有关`pttrackingmode`、`pttrackingversion`格式的详细信息，请参阅[API参考：清单服务器查询参数](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)。

## 服务器端广告跟踪{#server-side-ad-tracking}

使用此方法，广告跟踪数据完全在服务器端计算。 当更新客户端应用程序不可行时，此功能非常有用。 但是，服务器端广告跟踪可能与客户端播放活动不匹配。 例如，服务器会考虑在发送区段后播放广告，即使最终用户不视图整个广告。

要启用服务器端广告跟踪，请在[BootstrapAPI](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)中指定以下参数。

`pttrackingmode=sstm`

请参阅[BootstrapAPI](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)的`pttrackingmode`部分。

所有广告跟踪信标都与以下HTTP请求标头一起发送：

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

这些值包含客户端／播放器用户代理和客户端IP地址。

## 混合广告跟踪{#hybrid-ad-tracking}

这种方法类似于服务器端跟踪，但客户端应用程序也从PrimetimeAd Insertion请求sidecars以获取详细跟踪信息。 混合广告跟踪可以发送非线性广告，如叠加和与客户应用程序相伴的广告，同时仍依赖PrimetimeAd Insertion发送单个广告跟踪URL。
要启用混合广告跟踪，请参阅[BootstrapAPI](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)中的`pttrackingmode`参数。
