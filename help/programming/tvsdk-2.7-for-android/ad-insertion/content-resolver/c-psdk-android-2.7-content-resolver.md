---
description: 机会生成器通过流中的自定义标记、广告信令模式自定义标记等标识投放机会。 机会生成器将这些投放机会发送到内容解析器，内容解析器根据投放机会的属性和元数据来自定义内容/广告插入工作流。
title: 自定义机会生成器和内容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 概述 {#customize-opportunity-generators-and-content-resolvers-overview}

机会生成器通过流中的自定义标记、广告信令模式自定义标记等标识投放机会。 机会生成器将这些投放机会发送到内容解析器，内容解析器根据投放机会的属性和元数据来自定义内容/广告插入工作流。

TVSDK包含以下默认机会生成器：

* `ManifestCuesOpportunityGenerator` 从默认广告提示生成商机( `#EXT-X-CUE`)。

* `AdSignalingModeOpportunityGenerator` 为指定的ad信令模式生成初始机会。 这将忽略任何提示或定时元数据信息。
* `CustomMarkerOpportunityGenerator` 生成替换嵌入式C3广告的机会。
* `AuditudeResolver`的机会生成器会在延迟广告解决开启时生成机会。

TVSDK还包括默认内容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`，可与Primetime ad decisioning通信。

您可以覆盖默认的业务机会生成器和内容解析器，以按以下方式自定义广告工作流：

* 识别广告插入的自定义标记
* 创建自定义的广告提供商。
* 禁用内容。
