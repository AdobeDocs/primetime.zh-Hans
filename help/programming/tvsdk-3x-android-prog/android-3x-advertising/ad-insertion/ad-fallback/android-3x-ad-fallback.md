---
description: 对于启用回退规则的数字视频广告投放模板(VAST)广告（或创意）,TVSDK将无效媒体类型的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。
keywords: zero length ad;empty ad
seo-description: 对于启用回退规则的数字视频广告投放模板(VAST)广告（或创意）,TVSDK将无效媒体类型的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。
seo-title: VAST和VMAP广告的广告回退
title: VAST和VMAP广告的广告回退
uuid: 688f0b67-9f5b-4c21-ab33-86d21580fbe9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# VAST和VMAP广告的广告回退{#ad-fallback-for-vast-and-vmap-ads}

对于启用回退规则的数字视频广告投放模板(VAST)广告（或创意）,TVSDK将无效媒体类型的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。

VAST/数字视频多广告播放列表(VMAP)规范规定，对于启用了VAST回退的广告，空广告会自动触发回退广告的使用。 当VAST广告为空时，TVSDK在回退广告中查找有效的HLS媒体类型替换。 当包装器中的VAST广告的媒体类型无效时，TVSDK将此广告视为空。 您可以配置TVSDK是否应对VMAP内嵌的广告执行相同操作。 有关VAST `fallbackOnNoAd`功能的详细信息，请参阅[数字视频广告投放模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

>[!NOTE]
>
>**零长度广告** -当TVSDK遇到一个包含零持续时间广告的VAST响应，或者一个没有广告的广告中断时，它会为这些零长度广告中断触发AD_BREAK_开始/AD_BREAK_COMPLETE事件。*此行为仅适用于VOD流。* 即使您的应用程序使用SKIP广告策略，TVSDK也会触发这些事件。
>
>TVSDK对实时流&#x200B;*不*&#x200B;触发AD_BREAK_开始/AD_BREAK_COMPLETE事件，或者当用户使用滴答或试图通过零长广告时。