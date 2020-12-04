---
description: 机会生成器通过流中的自定义标记、以及信令模式自定义标记等来标识放置机会。 机会生成器将这些放置机会发送给内容解析器，内容解析器根据放置机会的属性和元数据自定义内容／广告插入工作流。
seo-description: 机会生成器通过流中的自定义标记、以及信令模式自定义标记等来标识放置机会。 机会生成器将这些放置机会发送给内容解析器，内容解析器根据放置机会的属性和元数据自定义内容／广告插入工作流。
seo-title: 自定义机会生成器和内容解析器
title: 自定义机会生成器和内容解析器
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 概述{#customize-opportunity-generators-and-content-resolvers-overview}

机会生成器通过流中的自定义标记、以及信令模式自定义标记等来标识放置机会。 机会生成器将这些放置机会发送给内容解析器，内容解析器根据放置机会的属性和元数据自定义内容／广告插入工作流。

TVSDK包括以下默认机会生成器：

* `ManifestCuesOpportunityGenerator` 根据默认广告提示()生成 `#EXT-X-CUE`机会。

* `AdSignalingModeOpportunityGenerator` 为指定的广告信令模式生成初始机会。这会忽略任何提示或定时元数据信息。
* `CustomMarkerOpportunityGenerator` 生成替换内置C3广告的机会。
* `AuditudeResolver`当延迟广告解决处于开启状态时，其机会生成器会产生机会。

TVSDK还包括默认内容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`，可与Primetime广告决策进行沟通。

您可以改写默认的业务机会生成器和内容解析器，以通过以下方式自定义广告工作流：

* 识别广告插入的自定义标记。 有关详细信息，请参阅[自定义机会生成器和内容解析器](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md)。
* 创建自定义广告提供商。
* 遮蔽内容。