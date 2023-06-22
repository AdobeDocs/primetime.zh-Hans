---
description: 当Primetime ad decisioningencounters为空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估后备广告以确定要返回的内容。
title: VAST和VMAP的广告回退行为
exl-id: 8145d928-5d38-40f1-8dc3-fee9b815465c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# VAST和VMAP的广告回退行为 {#ad-fallback-behavior-for-vast-and-vmap}

当Primetime ad decisioningencounters为空的或媒体类型对HLS无效的VAST广告（创意）时，它会评估后备广告以确定要返回的内容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒体类型为 `application/x-mpegURL` (M3U8)。

当存在独立的后备广告时，Primetime ad decisioningplug-in会按照以下顺序检查这些广告，并返回第一个具有有效媒体类型的广告：

1. 如果启用了重新打包，则会将第一次出现的具有无效媒体类型的广告视为其他无效媒体类型。

   如果重新打包失败，此过程适用于其他出现的广告。
1. 如果TVSDK找不到有效的后备广告，则会返回媒体类型无效的原始广告。
1. 如果返回的是具有有效MIME类型的后备广告而不是原始广告，则Primetime ad decisioningsite会将错误代码403发送到VAST错误URL（如果可用）。
1. 如果后备广告是包装器并返回多个广告，则仅返回具有正确媒体类型的广告。

>[!IMPORTANT]
>
>VAST包装器中的广告始终启用此行为。 对于VMAP中内联的VAST广告，默认情况下将禁用该行为，但您的应用程序可以启用它。
