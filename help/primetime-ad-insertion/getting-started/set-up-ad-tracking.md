---
title: 设置广告跟踪
description: 设置广告跟踪
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 设置广告跟踪 {#ser-up-ad-tracking}

大多数广告商需要了解他们的广告被查看的时间、时间和成功程度。 PrimetimeAd Insertion支持客户端、服务器端和混合广告跟踪，以便能够灵活地收集此信息。

## 使用VMAP/JSON进行客户端广告跟踪 {#client-side-ad-tracking-vmap-json}

在客户端广告跟踪中，服务器向客户端发送一个JSON、VMAP或清单内结构，用于指定跟踪事件和URL以及广告拼接播放列表。

要启用客户端广告跟踪，请在 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>设置 `pttrackingmode=simple` 将导致初始引导API请求返回JSON响应，而不是HLS或DASH文档。

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## 服务器端广告跟踪 {#server-side-ad-tracking}

使用此方法，广告跟踪数据完全在服务器端进行计算。 当更新客户端应用程序不可行时，这很有用。 但是，服务器端广告跟踪可能与客户端播放活动不匹配。 例如，服务器会考虑在投放区段后播放广告，即使最终用户未查看整个广告也是如此。

要启用服务器端广告跟踪，请在 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

请参阅 `pttrackingmode` 部分 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

所有广告跟踪信标均随以下HTTP请求标头一起发送：

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

这些值包含客户端/播放器用户代理和客户端IP地址。

## 混合广告跟踪 {#hybrid-ad-tracking}

此方法与服务器端跟踪类似，但客户端应用程序也从PrimetimeAd Insertion中请求辅助对象以获取详细的跟踪信息。 混合广告跟踪可以向客户端应用程序投放非线性广告，例如叠加和伴随，同时仍依赖于PrimetimeAd Insertion发送单个广告跟踪URL。
要启用混合广告跟踪，请参阅 `pttrackingmode` 中的参数 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
