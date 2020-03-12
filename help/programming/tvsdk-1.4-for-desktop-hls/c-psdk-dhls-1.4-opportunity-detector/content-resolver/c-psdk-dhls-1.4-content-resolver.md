---
description: 机会检测器是检测流中的自定义标记并识别放置机会的TVADK组件。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。
seo-description: 机会检测器是检测流中的自定义标记并识别放置机会的TVADK组件。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。
seo-title: 自定义机会检测器和内容解析器
title: 自定义机会检测器和内容解析器
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概述 {#customize-opportunity-detectors-and-content-resolvers-overiew}

机会检测器是检测流中的自定义标记并识别放置机会的TVADK组件。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。

TVSDK包括默认的机会检测器：

* `SpliceOutOpportunityDetector`，了解默认广告提示
* `AdSignalingModeOpportunityGenerator`，负责根据广告信令模式创建初始广告投放机会
* `SpliceOutOpportunityGenerator`，负责从任何#EXT-X-CUE标签创建广告投放机会

TVSDK还包含默认内容解析程序，该解析程序根据播放器项目中的元数据键提供要插入的内容：

* `AuditudeResolver`，能够与Adobe Primetime广告决策（以前称为Auditude）服务器通信并返回要放置的广告分段。

您可以通过以下方式覆盖默认的机会检测器和内容解析器以自定义广告工作流程：

* 添加对自定义标签检测的支持
* 识别广告插入的自定义标记
* 创建自定义广告提供商
* 遮蔽内容

