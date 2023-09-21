---
description: 您可以覆盖以下默认行为：使用自定义广告标记时，TVSDK搜寻广告的方式。
title: 控制对自定义广告标记进行搜索的播放行为
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 控制对自定义广告标记进行搜索的播放行为{#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以覆盖以下默认行为：使用自定义广告标记时，TVSDK搜寻广告的方式。

默认情况下，当用户搜寻或浏览因放置自定义广告标记而生成的广告部分时，TVSDK会跳过广告。 这可能与标准广告时间的当前播放行为不同。

当用户搜寻超过一个或多个自定义广告时，您可以指示TVSDK将播放头重新定位到最近跳过的自定义广告的开头。

1. 使用配置元数据实例 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 枚举设置为字符串值“true”（不是布尔值） `true`)。

1. 创建和配置 `MediaResource` 实例，将其他配置选项传递到 `TimeRangeCollection.toMetadata`. 此方法通过其他通用元数据结构接收其他配置选项。
