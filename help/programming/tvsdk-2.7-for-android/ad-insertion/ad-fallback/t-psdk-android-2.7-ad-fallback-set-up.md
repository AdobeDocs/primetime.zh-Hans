---
description: 当VMAP内联和包含无效媒体类型时，可启用回退。
seo-description: 当VMAP内联和包含无效媒体类型时，可启用回退。
seo-title: 定义VMAP内联广告的回退广告行为
title: 定义VMAP内联广告的回退广告行为
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 定义VMAP内联广告的回退广告行为 {#define-fallback-ad-behavior-for-vmap-inline-ads}

当VMAP内联和包含无效媒体类型时，可启用回退。

1. 设置 `setFallbackOnInvalidCreativeEnabled` 为 `true` 当线性／内联广告的媒体类型对于HLS无效时，VMAP将回退。

   默认值为 `false`。 如果线性广告因为媒体类型无效或广告无法重新打包而失败，则此标志允许Primetime广告决策遵循与广告为空VAST包装器一样的回退行为。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

