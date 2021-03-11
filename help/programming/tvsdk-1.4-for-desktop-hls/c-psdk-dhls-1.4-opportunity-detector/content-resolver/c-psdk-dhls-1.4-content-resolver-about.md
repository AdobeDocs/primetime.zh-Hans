---
description: TVSDK提供默认的机会生成器和内容解析器，将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）更改时间轴。
title: 机会生成器和内容解析器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供默认的机会生成器和内容解析器，将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）更改时间轴。

*`opportunity`*&#x200B;表示时间线上通常指示广告投放机会的关注点。 此机会还可以指示可能影响时间线的自定义操作，如封锁期。 *`opportunity generator`*&#x200B;标识时间轴中的特定机会（标记），并通知TVSDK这些机会已标记。 在`TimedMetadata`的时间轴中确定机会。 `SpliceOutOpportunityGenerator`基于为清单中检测到的每个广告标签创建的`TimedMetadata`对象创建机会，而`AdSignalingModeOpportunityGenerator`创建基于`MediaPlayerItem`类型及其关联的广告信令模式的初始机会。

当您的应用程序收到有关机会（标签）的通知时，您的应用程序可能会通过以下方式改变时间轴：插入一系列广告、切换到备用流（封锁期）或以其他方式编辑时间轴内容。 默认情况下，TVSDK调用相应的&#x200B;*`content resolver`*&#x200B;以实现所需的时间轴更改或操作。 您的应用程序可以使用默认的TVSDK广告内容解析程序或注册其自己的内容解析程序。

您还可以使用`PSDKConfig.adTags`为默认`SpliceOutOpportunityGenerator`类添加更多广告标记标记标记/提示并使用`PSDKConfig.setSubscribedTags`，以便TVSDK可以通知您的应用程序可能包含广告工作流程信息的其他标记。

自定义解析程序的一个可能用途是用于封锁期。 要处理这些期间，您的应用程序可以实施并注册一个负责处理封锁标签的封锁机会检测器。 当TVSDK遇到此标记时，它将轮询所有注册的内容解析器以找到处理指定标记的第一个解析器。 在此示例中，它是封锁内容解析程序，例如，它可以在标签指定的持续时间内，将播放器上的当前项目替换为替代内容。
