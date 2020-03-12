---
description: TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。
seo-description: TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。
seo-title: 机会生成器和内容解析器
title: 机会生成器和内容解析器
uuid: 9eaeeacf-9e7c-4ebb-a91e-fbc53e96d2c3
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。

A表 *`opportunity`* 示时间线上通常指示广告投放机会的兴趣点。 此机会还可以指示可能影响时间线的自定义操作，如封锁期。 An *`opportunity generator`* designs the specific opportunity(tags)in the timeline and notifications TVSDK thase opportunitys have be tagged. 在的时间轴中识别机会 `TimedMetadata`。 所述 `SpliceOutOpportunityGenerator` 机会基于为在清单中检测到的每个广告标签创建的对象而创建的机会，并且 `TimedMetadata` 基于类型及其关联的广告信令模式创建 `AdSignalingModeOpportunityGenerator``MediaPlayerItem` 初始机会。

当应用程序收到机会（标签）通知时，您的应用程序可能会通过（例如，插入一系列广告）切换到备用流（封锁期）或以其他方式编辑时间轴内容来更改时间轴。 默认情况下，TVSDK会调用相应的调 *`content resolver`* 用以实施所需的时间轴更改或操作。 您的应用程序可以使用默认的TVSDK广告内容解析程序或注册自己的内容解析程序。

您还可以使用 `PSDKConfig.adTags``SpliceOutOpportunityGenerator``PSDKConfig.setSubscribedTags` 为默认类添加更多广告标记标记标记／提示并使用，以便TVSDK可以通知您的应用程序，其他标记可能包含广告工作流程信息。

自定义解析程序的一个可能用途是用于封锁期。 要处理这些期间，您的应用程序可以实施并注册一个负责处理封锁标签的封锁机会检测器。 当TVSDK遇到此标记时，它将轮询所有注册内容解析器以找到处理指定标记的第一个解析器。 在此示例中，它是封锁内容解析程序，例如，它可以在标签指定的持续时间内，将播放器上的当前项目替换为替代内容。
