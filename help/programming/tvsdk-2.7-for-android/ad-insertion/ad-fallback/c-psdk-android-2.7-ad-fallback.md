---
description: 对于已启用后备规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK会将具有无效媒体类型的广告视为空广告，并尝试使用后备广告替换该广告。 您可以在某些方面配置回退行为。
keywords: 零长度广告；空广告
title: VAST和VMAP广告的广告回退
exl-id: 1fc04cac-e83f-4c1f-bf7b-1cbcb2135d53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# 概述 {#ad-fallback-for-vast-and-vmap-ads-overview}

对于已启用后备规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK会将具有无效媒体类型的广告视为空广告，并尝试使用后备广告替换该广告。 您可以在某些方面配置回退行为。

VAST/数字视频多个广告播放列表(VMAP)规范声明，对于启用了VAST回退的广告，空广告会自动触发回退广告的使用。 当VAST广告为空时，TVSDK会在后备广告中查找有效的HLS媒体类型替换。 当包装器中的VAST广告具有无效的媒体类型时，TVSDK会将此广告视为空。 您可以配置TVSDK是否应该对VMAP中的内联广告执行相同的操作。 有关VAST的更多信息 `fallbackOnNoAd` 功能，请参见 [数字视频广告投放模板(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**零长度广告**  — 当TVSDK遇到包含零持续时间广告或没有广告的广告时间的VAST响应时，它会为这些零长度的广告时间触发AD_BREAK_START / AD_BREAK_COMPLETE事件。 *此行为仅适用于VOD流。* 即使您的应用程序正在使用SKIP广告策略，TVSDK也会触发这些事件。
>
>TVSDK可以 *非* 为实时流触发AD_BREAK_START / AD_BREAK_COMPLETE事件，或者当用户使用trickplay或seek跳过零长度的广告时。
