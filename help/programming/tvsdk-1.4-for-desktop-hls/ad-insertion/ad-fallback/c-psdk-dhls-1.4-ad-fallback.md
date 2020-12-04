---
description: 对于启用回退规则的数字视频广告投放模板(VAST)广告（或创意）,TVSDK将无效媒体类型的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。
seo-description: 对于启用回退规则的数字视频广告投放模板(VAST)广告（或创意）,TVSDK将无效媒体类型的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。
seo-title: VAST和VMAP广告的广告回退
title: VAST和VMAP广告的广告回退
uuid: 7b44abf9-50cf-4e39-b594-ceb52208a865
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# VAST和VMAP广告的广告回退{#ad-fallback-for-vast-and-vmap-ads}

对于启用回退规则的数字视频广告投放模板(VAST)广告（或创意）,TVSDK将无效媒体类型的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。

VAST/数字视频多广告播放列表(VMAP)规范规定，对于启用VAST回退的广告，空广告会自动触发回退广告的使用。 当VAST广告为空时，TVSDK在回退广告中查找有效的HLS媒体类型替换。 当包装器中的VAST广告的媒体类型无效时，TVSDK将此广告视为空。 您可以配置TVSDK是否应对VMAP内嵌的广告执行相同操作。 有关VAST `fallbackOnNoAd`功能的详细信息，请参阅[数字视频广告投放模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

Primetime广告插入后端保留一组优先级，使其能够在同一VAST/VMAP响应中选择不同的媒体类型。 您可以在[CRS](../../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md)概述中进一步了解此优先级列表以及如何更改它。

## 定义VMAP内联广告{#define-fallback-ad-behavior-for-vmap-inline-ads}的回退广告行为

当VMAP内联广告包含无效媒体类型时，可以打开回退。

1. 将`fallbackOnInvalidCreative`设置为true，当线性／内联广告的媒体类型对HLS无效时，VMAP将回落。

   默认值为false。 如果线性广告失败，因为它的媒体类型无效，或者广告无法重新打包，则此标志允许Primetime广告决策遵循与广告是空VAST包装器相同的回退行为。

   ```
   var auditudeMetadata:AuditudeSettings = new AuditudeSettings(); 
   auditudeMetadata.fallbackOnInvalidCreative = true;
   ```

## VAST和VMAP {#ad-fallback-behavior-for-vast-and-vmap}的广告回退行为

当Primetime广告决策遇到空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估回退广告以确定要返回的内容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒体类型是`application/x-shockwave-flash`(VPAID)和`application/x-mpegURL`(m3u8)。

当有独立的回退广告时，Primetime广告决策插件会按以下顺序检查这些广告并返回具有有效媒体类型的第一个广告：

1. 如果启用重新打包，则具有无效媒体类型的广告的第一次出现会被视为其他无效媒体类型。

   如果重新打包失败，此过程将应用于广告的其他出现。
1. 如果TVSDK找不到有效的回退广告，则返回媒体类型无效的原始广告。
1. 如果返回的是具有有效MIME类型的回退广告，而不是原始广告，Primetime广告决策会将错误代码403发送到VAST错误URL（如果有）。
1. 如果回退广告是包装器并返回多个广告，则只返回具有正确媒体类型的广告。

>[!IMPORTANT]
>
>此行为始终适用于VAST包装中的广告。 对于VMAP内嵌的VAST广告，默认情况下会禁用该行为，但您的应用程序可以启用它。