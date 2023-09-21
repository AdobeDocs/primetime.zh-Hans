---
description: 当Primetime ad decisioningencounters一个空的VAST广告（创意）或一个媒体类型对HLS无效时，它评估后备广告以确定要返回的内容。
title: VAST和VMAP的广告回退行为
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# VAST和VMAP的广告回退行为 {#ad-fallback-behavior-for-vast-and-vmap}

当Primetime ad decisioningencounters一个空的VAST广告（创意）或一个媒体类型对HLS无效时，它评估后备广告以确定要返回的内容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒体类型为 `application/x-mpegURL` (M3U8)。

当存在独立的后备广告时，Primetime ad decisioningplug-in会按照以下顺序检查这些广告，并返回第一个具有有效媒体类型的广告：

1. 如果启用了重新打包，则会将第一次出现的具有无效媒体类型的广告视为其他无效媒体类型。

   如果重新打包失败，此过程适用于再次出现的广告。
1. 如果TVSDK未找到有效的后备广告，则会返回具有无效媒体类型的原始广告。
1. 如果返回的是具有有效MIME类型的后备广告而不是原始广告，则Primetime ad decisioningsent将错误代码403发送到VAST错误URL（如果可用）。
1. 如果后备广告是包装器并返回多个广告，则仅返回具有正确媒体类型的广告。

>[!IMPORTANT]
>
>始终为VAST包装器中的广告启用此行为。 对于在VMAP中内联的VAST广告，默认情况下将禁用该行为，但您的应用程序可以启用它。
