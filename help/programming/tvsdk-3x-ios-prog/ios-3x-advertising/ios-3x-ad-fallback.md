---
description: 对于启用了回退规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK会将具有无效媒体类型的广告视为空广告，并尝试在其位置使用回退广告。 您可以在某些方面配置回退行为。
title: VAST和VMAP广告的广告回退
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# VAST和VMAP广告的广告回退 {#ad-fallback-for-vast-and-vmap-ads}

对于启用了回退规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK会将具有无效媒体类型的广告视为空广告，并尝试在其位置使用回退广告。 您可以在某些方面配置回退行为。

VAST/数字视频多广告播放列表(VMAP)规范规定，对于启用了VAST回退的广告，空广告会自动触发回退广告的使用。 当VAST广告为空时，TVSDK会在后备广告中查找有效的HLS媒体类型替换。 当包装器中的VAST广告具有无效的媒体类型时，TVSDK会将此广告视为空。 您可以配置TVSDK是否应该对VMAP中的内联广告执行相同的操作。 有关VAST的详细信息 `fallbackOnNoAd` 功能，请参见 [数字视频广告服务模板(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## 为VMAP内联广告定义后备广告行为 {#section_D90BB3C6E539472EABF000C0F616DBE2}

当VMAP内联广告包含无效的媒体类型时，您可以启用回退。

1. 设置 `FallbackOnInvalidCreativeEnabled` 到 `YES` 当线性/内联广告的媒体类型对HLS无效时，让VMAP回退。

   >[!NOTE]
   >
   >默认值为NO。 如果线性广告由于媒体类型无效或无法重新打包而失败，则此标记允许Primetime广告决策遵循相同的回退行为，就像广告是空VAST包装器一样。

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## VAST和VMAP的广告回退行为 {#section_5B6716CC49CC4C40964CFE9F122C57A6}

当Primetime ad Decisioning遇到空的VAST广告（创意广告）或媒体类型对HLS无效时，它会评估后备广告以确定要返回的内容。

在TVSDK中，唯一有效的媒体类型为 `application/x-mpegURL` (M3U8)。

当存在独立的后备广告时，Primetime ad decisioning插件会按照以下顺序检查这些广告，并返回第一个具有有效媒体类型的广告：

1. 如果启用了重新打包，则会将第一次出现的具有无效媒体类型的广告视为其他无效媒体类型。

   如果重新打包失败，此过程适用于再次出现的广告。
1. 如果TVSDK未找到有效的后备广告，则会返回具有无效媒体类型的原始广告。
1. 如果返回的是具有有效MIME类型的后备广告而不是原始广告，Primetime广告决策会向VAST错误URL发送错误代码403（如果可用）。
1. 如果后备广告是包装器并返回多个广告，则仅返回具有正确媒体类型的广告。

>[!IMPORTANT]
>
>始终为VAST包装器中的广告启用此行为。 对于在VMAP中内联的VAST广告，默认情况下将禁用该行为，但您的应用程序可以启用它。
