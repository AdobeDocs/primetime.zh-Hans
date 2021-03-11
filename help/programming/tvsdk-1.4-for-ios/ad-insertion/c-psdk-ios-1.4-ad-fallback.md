---
description: 对于启用了回退规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK将具有无效媒体类型的广告视为空广告，并尝试使用回退广告代替广告。 您可以配置回退行为的某些方面。
title: VAST和VMAP广告的广告回退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# VAST和VMAP广告的广告回退{#ad-fallback-for-vast-and-vmap-ads}

对于启用了回退规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK将具有无效媒体类型的广告视为空广告，并尝试使用回退广告代替广告。 您可以配置回退行为的某些方面。

VAST/数字视频多广告播放列表(VMAP)规范规定，对于启用VAST回退的广告，空广告会自动触发回退广告的使用。 当VAST广告为空时，TVSDK在回退广告中查找有效的HLS媒体类型替换。 包装器中的VAST广告的媒体类型无效时，TVSDK将此广告视为空。 您可以配置TVSDK是否应对VMAP内联广告执行相同操作。 有关VAST `fallbackOnNoAd`功能的详细信息，请参阅[数字视频广告投放模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

## 定义VMAP内联广告{#section_D90BB3C6E539472EABF000C0F616DBE2}的回退广告行为

当VMAP内联和包含无效媒体类型时，可以打开回退。

1. 将`FallbackOnInvalidCreativeEnabled`设置为`YES`，以使VMAP在线性/内联广告的媒体类型对HLS无效时回落。

   >[!NOTE]
   >
   >默认值为NO。 如果线性广告因为媒体类型无效或无法重新打包广告而失败，则此标志允许Primetime广告决策遵循与广告为空VAST包装器相同的回退行为。

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## VAST和VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}的广告回退行为

当Primetime广告决策遇到空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估回退广告以确定要返回的内容。

在TVSDK中，唯一有效的媒体类型是`application/x-mpegURL`(M3U8)。

当有独立的回退广告时，Primetime广告决策插件会按以下顺序检查这些广告并返回具有有效媒体类型的第一则广告：

1. 如果启用重新打包，则具有无效媒体类型的广告的第一次出现会被视为其他无效媒体类型。

   如果重新打包失败，则此过程适用于广告的其他实例。
1. 如果TVSDK找不到有效的回退广告，则返回媒体类型无效的原始广告。
1. 如果返回的是具有有效MIME类型的回退广告，而不是原始广告，Primetime广告决策会将错误代码403发送到VAST错误URL（如果可用）。
1. 如果回退广告是包装器并返回多个广告，则只返回具有正确媒体类型的广告。

>[!IMPORTANT]
>
>此行为始终支持VAST包装中的广告。 对于VMAP内嵌的VAST广告，默认情况下会禁用该行为，但您的应用程序可以启用它。

