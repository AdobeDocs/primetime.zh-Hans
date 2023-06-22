---
description: 当VMAP内联广告包含无效的媒体类型时，您可以启用回退。
title: 为VMAP内联广告定义后备广告行为
exl-id: 50de85b0-df2b-422f-893c-dfa641b4901e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 为VMAP内联广告定义后备广告行为 {#define-fallback-ad-behavior-for-vmap-inline-ads}

当VMAP内联广告包含无效的媒体类型时，您可以启用回退。

1. 设置 `setFallbackOnInvalidCreativeEnabled` 到 `true` 当线性/内联广告的媒体类型对HLS无效时，让VMAP回退。

   默认值为 `false`. 如果线性广告由于媒体类型无效或由于无法重新打包而失败，则此标记允许Primetime广告决策遵循相同的回退行为，就像广告是空的VAST包装一样。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
