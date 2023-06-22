---
description: 机会生成器通过流中的自定义标记、信令模式自定义标记等标识放置机会。 机会生成器将这些投放机会发送给内容解析器，内容解析器根据投放机会的属性和元数据自定义内容/广告插入工作流。
title: 自定义机会生成器和内容解析器
exl-id: 5d0ebaa6-4708-4602-b9d7-882c389fb030
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 概述 {#customize-opportunity-generators-and-content-resolvers-overview}

机会生成器通过流中的自定义标记、信令模式自定义标记等标识放置机会。 机会生成器将这些投放机会发送给内容解析器，内容解析器根据投放机会的属性和元数据自定义内容/广告插入工作流。

TVSDK包含以下默认机会生成器：

* `ManifestCuesOpportunityGenerator` 从默认广告提示生成商机( `#EXT-X-CUE`)。

* `AdSignalingModeOpportunityGenerator` 为指定的广告信令模式生成初始机会。 这将忽略任何提示或定时元数据信息。
* `CustomMarkerOpportunityGenerator` 会生成替换内置C3广告的机会。
* `AuditudeResolver`的opportunity generator会在懒惰的广告解决开启时产生机会。

TVSDK还包括默认内容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`，可以与Primetime ad decisioning通信。

您可以覆盖默认机会生成器和内容解析器，以按以下方式自定义广告工作流：

* 识别广告插入的自定义标记。 有关更多信息，请参阅 [自定义机会生成器和内容解析器](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* 创建自定义的广告提供商。
* 禁止显示内容。
