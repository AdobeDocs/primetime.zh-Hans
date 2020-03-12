---
description: 当VMAP内联和包含无效媒体类型时，可启用回退。
seo-description: 当VMAP内联和包含无效媒体类型时，可启用回退。
seo-title: 定义VMAP内联广告的回退广告行为
title: 定义VMAP内联广告的回退广告行为
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 定义VMAP内联广告的回退广告行为 {#define-fallback-ad-behavior-for-vmap-inline-ads}

当VMAP内联和包含无效媒体类型时，可启用回退。

1. 设置 `setFallbackOnInvalidCreativeEnabled` 为 `true` 当线性／内联广告的媒体类型对于HLS无效时，VMAP将回退。

   默认值为 `false`。 如果线性广告因为媒体类型无效或广告无法重新打包而失败，则此标志允许Primetime广告决策遵循与广告为空VAST包装器一样的回退行为。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
