---
description: 当Primetime广告决策遇到空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估回退广告以确定要返回的内容。
seo-description: 当Primetime广告决策遇到空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估回退广告以确定要返回的内容。
seo-title: VAST和VMAP的广告回退行为
title: VAST和VMAP的广告回退行为
uuid: 50e17372-fd29-4792-aafa-8f9c21cc42c6
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# VAST和VMAP的广告回退行为 {#ad-fallback-behavior-for-vast-and-vmap}

当Primetime广告决策遇到空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估回退广告以确定要返回的内容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒体类 `application/x-mpegURL` 型是(M3U8)。

当有独立的备用广告时，Primetime广告决策插件会按以下顺序检查这些广告并返回具有有效媒体类型的第一个广告：

1. 如果启用了重新打包，则具有无效媒体类型的广告的第一次出现将被视为其他无效媒体类型。

   如果重新打包失败，则此过程适用于广告的其他出现。
1. 如果TVSDK未找到有效的回退广告，则返回媒体类型无效的原始广告。
1. 如果返回的是具有有效MIME类型的回退广告而不是原始广告，则Primetime广告决策会将错误代码403发送到VAST错误URL（如果有）。
1. 如果回退广告是包装器并返回多个广告，则只返回具有正确媒体类型的广告。

>[!IMPORTANT]
>
>此行为始终针对VAST包装中的广告启用。 对于VMAP中内嵌的VAST广告，默认情况下会禁用该行为，但您的应用程序可以启用它。

