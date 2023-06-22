---
description: 机会检测器是一个浏览器TVSDK组件，可检测流中的自定义标记并识别投放机会。 这些机会将发送给内容解析器，内容解析器根据版面机会属性和元数据自定义内容/广告插入工作流。
title: 定制机会检测器和内容解析器
exl-id: 1866ed53-acfc-45d3-941e-0ed171aa038b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 概述 {#customize-opportunity-detectors-and-content-resolvers-overview}

机会检测器是一个浏览器TVSDK组件，可检测流中的自定义标记并识别投放机会。 这些机会将发送给内容解析器，内容解析器根据版面机会属性和元数据自定义内容/广告插入工作流。

浏览器TVSDK包含以下默认机会检测器：

* `AdSignalingModeOpportunityGenerator`，根据广告信号模式创建初始广告投放机会。
* `ManifestCuesOpportunityGenerator`，从任何剪切标记创建广告投放机会。

浏览器TVSDK还包括默认内容解析器，例如 `AuditudeResolver`，提供将根据播放器项中的元数据键插入的内容。 `AuditudeResolver` 能够与Adobe Primetime ad decisioning服务器通信并返回要投放的广告时间。

您可以通过以下方式覆盖默认机会检测器和内容解析器来自定义广告工作流：

* 添加对自定义标记检测的支持
* 识别广告插入的自定义标记
* 创建自定义的广告提供商
