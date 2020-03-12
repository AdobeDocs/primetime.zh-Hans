---
description: 在使用自定义广告标记时，您可以覆盖TVSDK搜索广告时的默认行为。
seo-description: 在使用自定义广告标记时，您可以覆盖TVSDK搜索广告时的默认行为。
seo-title: 控制用于搜索自定义广告标记的播放行为
title: 控制用于搜索自定义广告标记的播放行为
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 控制用于搜索自定义广告标记的播放行为{#control-playback-behavior-for-seeking-over-custom-ad-markers}

在使用自定义广告标记时，您可以覆盖TVSDK搜索广告时的默认行为。

默认情况下，当用户搜索自定义广告标记所产生的广告部分或以前的广告部分时，TVSDK会跳过广告。 这可能与标准广告中断的当前播放行为不同。

当用户搜索超过一个或多个自定义广告时，您可以告诉TVSDK将播放头重新定位到最近跳过的自定义广告的开头。

1. 配置元数据实例，将 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 枚举设置为字符串值“true”(而非布尔值 `true`)。

1. 创建并配置一 `MediaResource` 个实例，将其他配置选项传递给 `TimeRangeCollection.toMetadata`。 此方法通过另一个通用元数据结构接收其他配置选项。

