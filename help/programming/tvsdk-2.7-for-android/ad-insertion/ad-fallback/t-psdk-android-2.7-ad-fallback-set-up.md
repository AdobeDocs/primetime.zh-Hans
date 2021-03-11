---
description: 可以在VMAP内联和包含无效媒体类型时启用回退。
title: 定义VMAP内联广告的回退广告行为
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# 定义VMAP内联广告{#define-fallback-ad-behavior-for-vmap-inline-ads}的回退广告行为

可以在VMAP内联和包含无效媒体类型时启用回退。

1. 将`setFallbackOnInvalidCreativeEnabled`设置为`true`，以使VMAP在线性/内联广告的媒体类型对HLS无效时回落。

   默认值为`false`。 如果线性广告因为媒体类型无效或无法重新打包广告而失败，则此标志允许Primetime广告决策遵循与广告是空VAST包装器相同的回退行为。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

