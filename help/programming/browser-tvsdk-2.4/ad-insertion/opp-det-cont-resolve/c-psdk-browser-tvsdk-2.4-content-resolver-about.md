---
description: 浏览器TVSDK提供了在时间轴中放置广告的默认机会生成器和内容解析器，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会，更改时间线。
title: 机会生成器和内容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

浏览器TVSDK提供了在时间轴中放置广告的默认机会生成器和内容解析器，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会，更改时间线。

An *`opportunity`* 表示时间轴上的兴趣点，通常指示广告投放机会。 此机会还可以指示可能影响时间线的自定义操作。 An *`opportunity generator`* 会识别时间轴中的特定机会（标记），并通知TVSDK这些机会已标记。

在的时间表中识别机会 `TimedMetata`. 此 `ManifestCuesOpportunityGenerator` 根据以下内容创建机会 `TimedMetadata` 为每个剪切出广告标记创建的对象(在 `MediaPlayerItemConfig.adTags`)。 此 `AdSignalingModeOpportunityGenerator` 创建基于 `MediaPlayerItem` 类型及其关联的广告信令模式。

>[!TIP]
>
>如果 `AdvertisingMetadata.livePreroll` 或 `AdvertisingMetadata.preroll` 属性已设置， `AdSignalingModeOpportunityGenerator` 为实时流生成前置机会。

当您的应用程序收到有关商机（标记）的通知时，您的应用程序可能会更改时间线，例如，通过插入一系列广告。 默认情况下，浏览器TVSDK调用相应的 *`content resolver`* 实施所需的时间线更改或操作。 您的应用程序可以使用默认的浏览器TVSDK播发内容解析程序或注册自己的内容解析程序。

您还可以使用 `MediaPlayerItemConfig.adTags` 为默认添加更多广告标记标记/提示 `ManifestCuesOpportunityGenerator` 类和使用 `MediaPlayerItemConfig.subscribedTags` 以便TVSDK能够将可能包含广告工作流信息的其他标记通知您的应用程序。

>[!TIP]
>
>默认值 `MediaPlayerItemConfig.adTags` 和 `MediaPlayerItemConfig.subscribeTags` 是 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
