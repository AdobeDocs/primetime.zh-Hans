---
description: TVSDK提供了在时间轴中放置广告的默认机会生成器和内容解析器，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（例如封锁期的指示器）更改时间线。
title: 机会生成器和内容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供了在时间轴中放置广告的默认机会生成器和内容解析器，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（例如封锁期的指示器）更改时间线。

An *`opportunity`* 表示时间轴上的兴趣点，通常指示广告投放机会。 此机会还可以指示可能影响时间线的自定义操作，如封锁期。 An *`opportunity generator`* 会识别时间轴中的特定机会（标记），并通知TVSDK这些机会已标记。 在的时间表中识别机会 `TimedMetadata`. 此 `SpliceOutOpportunityGenerator` 根据以下内容创建机会 `TimedMetadata` 在清单中检测到的每个广告标记创建的对象，以及 `AdSignalingModeOpportunityGenerator` 创建基于 `MediaPlayerItem` 类型及其关联的广告信令模式。

当您的应用程序收到有关机会（标记）的通知时，您的应用程序可能会更改时间线，例如，通过插入一系列广告、切换到备用流（中断）或编辑时间线内容。 默认情况下，TVSDK调用相应的 *`content resolver`* 实施所需的时间线更改或操作。 您的应用程序可以使用默认的TVSDK播发内容解析程序或注册自己的内容解析程序。

您还可以使用 `PSDKConfig.adTags` 为默认添加更多广告标记标记/提示 `SpliceOutOpportunityGenerator` 类和使用 `PSDKConfig.setSubscribedTags` 以便TVSDK能够将可能包含广告工作流信息的其他标记通知您的应用程序。

自定义解析器的一种可能用途是封锁期。 要处理这些周期，您的应用程序可以实施并注册一个负责处理中断标记的中断机会检测器。 当TVSDK遇到此标记时，它会轮询所有已注册的内容解析器，以查找第一个处理指定标记的内容解析器。 在本例中，它就是中断内容解析器，例如，它可以用播放器上的替代内容替换当前项目，持续时间由标记指定。
