---
description: 机会检测器是一个TVADK组件，它检测流中的自定义标签并识别投放机会。 这些机会将发送到内容解析器，内容解析器根据版面机会属性和元数据来自定义内容/广告插入工作流。
title: 定制机会检测器和内容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 概述 {#customize-opportunity-detectors-and-content-resolvers-overiew}

机会检测器是一个TVADK组件，它检测流中的自定义标签并识别投放机会。 这些机会将发送到内容解析器，内容解析器根据版面机会属性和元数据来自定义内容/广告插入工作流。

TVSDK包含默认机会检测器：

* `SpliceOutOpportunityDetector`，了解默认广告提示
* `AdSignalingModeOpportunityGenerator`，负责根据广告信令模式创建初始广告投放机会
* `SpliceOutOpportunityGenerator`，负责从任何#EXT-X-CUE标记中创建广告投放机会

TVSDK还包括一个默认内容解析器，该解析器根据播放器项中的元数据键提供要插入的内容：

* `AuditudeResolver`，能够与Adobe Primetime ad decisioning(以前称为Auditude)服务器通信并返回要投放的广告时间。

您可以通过以下方式覆盖默认机会检测器和内容解析器以自定义广告工作流：

* 添加对自定义标记检测的支持
* 识别广告插入的自定义标记
* 创建自定义广告提供商
* 禁用内容
