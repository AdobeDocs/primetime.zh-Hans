---
description: 使用自定义广告标记时，您可以覆盖TVSDK搜寻广告的默认行为。
title: 控制对自定义广告标记进行搜寻的播放行为
exl-id: c821e0be-1490-4b5f-8f9f-bffdfb1a982d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 控制对自定义广告标记进行搜寻的播放行为{#control-playback-behavior-for-seeking-over-custom-ad-markers}

使用自定义广告标记时，您可以覆盖TVSDK搜寻广告的默认行为。

默认情况下，当用户搜寻或浏览因放置自定义广告标记而生成的广告部分时，TVSDK会跳过广告。 这可能与标准广告时间的当前播放行为不同。

当用户搜寻超过一个或多个自定义广告时，您可以指示TVSDK将播放头重新定位到最近跳过的自定义广告的开头。

1. 使用配置元数据实例 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 枚举设置为字符串值“true”（不是布尔值） `true`)。

1. 创建和配置 `MediaResource` 实例，将其他配置选项传递到 `TimeRangeCollection.toMetadata`. 此方法通过其他通用元数据结构接收其他配置选项。
