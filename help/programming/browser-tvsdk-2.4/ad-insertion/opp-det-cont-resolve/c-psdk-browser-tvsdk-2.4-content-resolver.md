---
description: 机会检测器是一个浏览器TVSDK组件，可检测流中的自定义标记并确定投放机会。 这些机会将发送到内容解析器，内容解析器根据版面机会属性和元数据来自定义内容/广告插入工作流。
title: 定制机会检测器和内容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 概述 {#customize-opportunity-detectors-and-content-resolvers-overview}

机会检测器是一个浏览器TVSDK组件，可检测流中的自定义标记并确定投放机会。 这些机会将发送到内容解析器，内容解析器根据版面机会属性和元数据来自定义内容/广告插入工作流。

浏览器TVSDK包含以下默认机会检测器：

* `AdSignalingModeOpportunityGenerator`，将根据广告信号模式创建初始广告投放机会。
* `ManifestCuesOpportunityGenerator`，从任何剪切标记创建广告投放机会。

浏览器TVSDK还包括默认的内容解析器，例如 `AuditudeResolver`，提供将根据播放器项中的元数据键插入的内容。 `AuditudeResolver` 能够与Adobe Primetime ad decisioning服务器通信并返回要投放的广告时间。

您可以通过以下方式覆盖默认机会检测器和内容解析器以自定义广告工作流：

* 添加对自定义标记检测的支持
* 识别广告插入的自定义标记
* 创建自定义广告提供商
