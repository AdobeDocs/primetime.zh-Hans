---
description: 对于启用了回退规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK将具有无效媒体类型的广告视为空广告，并尝试使用回退广告代替广告。 您可以配置回退行为的某些方面。
keywords: 零长广告；空广告
title: VAST和VMAP广告的广告回退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# 概述{#ad-fallback-for-vast-and-vmap-ads-overview}

对于启用了回退规则的数字视频广告服务模板(VAST)广告（或创意），TVSDK将具有无效媒体类型的广告视为空广告，并尝试使用回退广告代替广告。 您可以配置回退行为的某些方面。

VAST/数字视频多广告播放列表(VMAP)规范规定，对于启用了VAST回退的广告，空广告会自动触发回退广告的使用。 当VAST广告为空时，TVSDK在回退广告中查找有效的HLS媒体类型替换。 包装器中的VAST广告的媒体类型无效时，TVSDK将此广告视为空。 您可以配置TVSDK是否应对VMAP内联广告执行相同操作。 有关VAST `fallbackOnNoAd`功能的详细信息，请参阅[数字视频广告投放模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

>[!NOTE]
>
>**零长度广告**  — 当TVSDK遇到一个包含零持续时间广告的VAST响应，或一个没有广告的广告中断时，它会为这些零长度广告中断触发AD_BREAK_开始/AD_BREAK_COMPLETE事件。*此行为仅适用于VOD流。* 即使您的应用程序使用SKIP广告策略，TVSDK也会触发这些事件。
>
>TVSDK会&#x200B;*不*&#x200B;触发AD_BREAK_开始/AD_BREAK_COMPLETE事件，或者当用户使用变戏或试图超越零长广告时。

