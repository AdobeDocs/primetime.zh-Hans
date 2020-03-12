---
description: TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。
seo-description: TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。
seo-title: 机会生成器和内容解析器
title: 机会生成器和内容解析器
uuid: 35823336-5338-4cdc-8778-e73cd1d05251
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 机会生成器和内容解析器 {#opportunity-generators-and-content-resolvers}

TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。

A表 *`opportunity`* 示时间线上通常指示广告投放机会的兴趣点。 此机会还可以指示可能影响时间线的自定义操作，如封锁期。 An *`opportunity generator`* designs the specific opportunity(tags)in the timeline and notifications TVSDK thase opportunitys have be tagged. 在时间轴中，通过包括非标准（非HLS）标记来识别机会。

当您的应用程序收到机会通知时，您的应用程序可能会通过插入一系列广告、切换到备用流（封锁期）或以其他方式编辑时间轴内容来更改时间轴。 默认情况下，TVSDK会调用相应的调 *`content resolver`* 用以实施所需的时间轴更改或操作。 您的应用程序可以使用默认的TVSDK广告内容解析程序或注册自己的内容解析程序。

您还可以使用添 `MediaPlayerItemConfig.setAdTags``MediaPlayerItemConfig.subscribedTags` 加更多广告标记标记标记／提示，以便TVSDK能够识别和使用您的应用程序，并通知您的应用程序可能包含广告工作流程信息的其他标记。

自定义解析程序的一个可能用途是用于封锁期。 要处理这些期间，您的应用程序可以实施并注册一个负责处理封锁标签的封锁机会检测器。 当TVSDK遇到此标记时，它将轮询所有注册内容解析器以找到处理指定标记的第一个解析器。 在此示例中，它是封锁内容解析程序，例如，它可以在标签指定的持续时间内，将播放器上的当前项目替换为替代内容。
