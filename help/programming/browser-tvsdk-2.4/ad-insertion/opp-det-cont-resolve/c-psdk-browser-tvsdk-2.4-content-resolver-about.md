---
description: 浏览器TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会来更改时间轴。
seo-description: 浏览器TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会来更改时间轴。
seo-title: 机会生成器和内容解析器
title: 机会生成器和内容解析器
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

浏览器TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会来更改时间轴。

A表 *`opportunity`* 示时间线上通常指示广告投放机会的兴趣点。 此机会还可以指示可能影响时间线的自定义操作。 An *`opportunity generator`* designs the specific opportunity(tags)in the timeline and notifications TVSDK thase opportunitys have be tagged.

在的时间轴中识别机会 `TimedMetata`。 该 `ManifestCuesOpportunityGenerator` 方法基于为清单中 `TimedMetadata` 检测到的每个拼接广告标签(在中 `MediaPlayerItemConfig.adTags`)创建的对象来创建机会。 所述 `AdSignalingModeOpportunityGenerator` 初始机会基于所述类型及其关联的广 `MediaPlayerItem` 告信令模式来创建。

>[!TIP]
>
>如果设 `AdvertisingMetadata.livePreroll` 置了或 `AdvertisingMetadata.preroll` 属性，则 `AdSignalingModeOpportunityGenerator` 会为实时流生成预置机会。

当您的应用程序收到机会（标签）通知时，您的应用程序可能会通过插入一系列广告来更改时间轴。 默认情况下，浏览器TVSDK会调用相应的调 *`content resolver`* 用，以实施所需的时间轴更改或操作。 您的应用程序可以使用默认的浏览器TVSDK广告内容解析程序或注册自己的内容解析程序。

您还可以使用 `MediaPlayerItemConfig.adTags` 为默认类添加更多广告标记标记标记／提示，并使用 `ManifestCuesOpportunityGenerator``MediaPlayerItemConfig.subscribedTags` ，以便TVSDK可以通知您的应用程序可能包含广告工作流程信息的其他标记。

>[!TIP]
>
>和的默 `MediaPlayerItemConfig.adTags` 认 `MediaPlayerItemConfig.subscribeTags` 值 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`。

