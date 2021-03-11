---
description: 机会生成器通过流中的自定义标记、以及信令模式自定义标记等来标识放置机会。 业务机会生成器将这些业务机会发送给内容解析器，内容解析器根据业务机会的属性和元数据定制内容/广告插入工作流。
title: 自定义机会生成器和内容解析器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# 概述{#customize-opportunity-generators-and-content-resolvers-overview}

机会生成器通过流中的自定义标记、以及信令模式自定义标记等来标识放置机会。 业务机会生成器将这些业务机会发送给内容解析器，内容解析器根据业务机会的属性和元数据定制内容/广告插入工作流。

TVSDK包括以下默认机会生成器：

* `ManifestCuesOpportunityGenerator` 根据默认广告提示()生成 `#EXT-X-CUE`机会。

* `AdSignalingModeOpportunityGenerator` 为指定的广告信令模式生成初始机会。这会忽略任何提示或定时元数据信息。
* `CustomMarkerOpportunityGenerator` 可以产生取代C3广告的机会。
* `AuditudeResolver`当延迟广告解决打开时，s opportunity generator会产生机会。

TVSDK还包含默认内容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`，可与Primetime广告决策沟通。

您可以覆盖默认的业务机会生成器和内容解析器，以通过以下方式自定义广告工作流：

* 识别广告插入的自定义标记
* 创建自定义广告提供商。
* 遮蔽内容。