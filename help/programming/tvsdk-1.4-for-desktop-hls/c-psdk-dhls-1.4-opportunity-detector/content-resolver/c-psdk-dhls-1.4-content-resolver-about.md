---
description: TVSDK提供了在时间轴中放置广告的默认机会生成器和内容解析器，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（例如封锁期的指示器）更改时间线。
title: 机会生成器和内容解析器
exl-id: 6daf7ff4-10c4-4750-8592-94a2be489473
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供了在时间轴中放置广告的默认机会生成器和内容解析器，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（例如封锁期的指示器）更改时间线。

An *`opportunity`* 表示时间轴上的目标点，通常指示广告投放机会。 此机会还可以指示可能影响时间线的自定义操作，例如封锁期。 An *`opportunity generator`* 识别时间线中的特定机会（标记），并通知TVSDK这些机会已标记。 在的时间表中识别机会 `TimedMetadata`. 此 `SpliceOutOpportunityGenerator` 根据以下内容创造机会 `TimedMetadata` 在清单中检测到的为每个广告标记创建的对象，以及 `AdSignalingModeOpportunityGenerator` 创建基于 `MediaPlayerItem` 类型及其关联的广告信令模式。

当您的应用程序收到有关机会（标记）的通知时，您的应用程序可能会更改时间线，例如，通过插入一系列广告、切换到备用流（中断）或编辑时间线内容等。 默认情况下，TVSDK会调用相应的 *`content resolver`* 以实施所需的时间线更改或操作。 您的应用程序可以使用默认的TVSDK播发内容解析程序或注册自己的内容解析程序。

您还可以使用 `PSDKConfig.adTags` 为默认添加更多广告标记标记/提示 `SpliceOutOpportunityGenerator` 类与使用 `PSDKConfig.setSubscribedTags` 以便TVSDK可以将可能包含广告工作流信息的其他标记通知您的应用程序。

自定义解析器的一种可能用途是封锁期。 要处理这些时段，您的应用程序可以实施并注册一个负责处理中断标记的中断机会检测器。 当TVSDK遇到此标记时，它会轮询所有注册的内容解析器，以查找第一个处理指定标记的内容解析器。 在本例中，它就是封锁内容解析程序，例如，它可以用播放器上的替代内容替换当前项目，持续时间由标记指定。
