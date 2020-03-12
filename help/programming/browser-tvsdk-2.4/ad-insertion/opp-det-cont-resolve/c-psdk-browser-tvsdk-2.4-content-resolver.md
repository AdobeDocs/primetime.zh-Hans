---
description: 机会检测器是浏览器TVSDK组件，它检测流中的自定义标记并识别放置机会。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。
seo-description: 机会检测器是浏览器TVSDK组件，它检测流中的自定义标记并识别放置机会。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。
seo-title: 自定义机会检测器和内容解析器
title: 自定义机会检测器和内容解析器
uuid: d4926933-5966-4cd8-8050-c81c5e3c8545
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 概述 {#customize-opportunity-detectors-and-content-resolvers-overview}

机会检测器是浏览器TVSDK组件，它检测流中的自定义标记并识别放置机会。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。

浏览器TVSDK包括以下默认机会检测器：

* `AdSignalingModeOpportunityGenerator`这将基于广告信令模式创造初始广告投放机会。
* `ManifestCuesOpportunityGenerator`，这会从任何拼接标签创建广告投放机会。

浏览器TVSDK还包括默认内容解析器，例如 `AuditudeResolver`，提供将根据播放器项中的元数据键插入的内容。 `AuditudeResolver` 能够与Adobe Primetime广告决策服务器通信并返回要放置的广告分段。

您可以通过以下方式覆盖默认的机会检测器和内容解析器以自定义广告工作流程：

* 添加对自定义标签检测的支持
* 识别广告插入的自定义标记
* 创建自定义广告提供商

