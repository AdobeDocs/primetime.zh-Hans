---
description: 浏览器TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中确定的机会更改时间轴。
seo-description: 浏览器TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中确定的机会更改时间轴。
seo-title: 机会生成器和内容解析器
title: 机会生成器和内容解析器
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

浏览器TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中确定的机会更改时间轴。

*`opportunity`*&#x200B;表示时间线上通常指示广告投放机会的兴趣点。 此机会还可以指示可能影响时间线的自定义操作。 *`opportunity generator`*&#x200B;在时间轴中标识特定机会（标记），并通知TVSDK这些机会已标记。

在`TimedMetata`的时间轴中确定机会。 `ManifestCuesOpportunityGenerator`根据为清单中检测到的每个拼接广告标签（在`MediaPlayerItemConfig.adTags`中）创建的`TimedMetadata`对象创建机会。 `AdSignalingModeOpportunityGenerator`创建基于`MediaPlayerItem`类型及其关联的广告信令模式的初始机会。

>[!TIP]
>
>如果设置了`AdvertisingMetadata.livePreroll`或`AdvertisingMetadata.preroll`属性，`AdSignalingModeOpportunityGenerator`将为实时流生成前置机会。

当您的应用程序收到机会（标记）通知时，您的应用程序可能会通过插入一系列广告等方式改变时间轴。 默认情况下，浏览器TVSDK调用相应的&#x200B;*`content resolver`*&#x200B;来实施所需的时间轴更改或操作。 您的应用程序可以使用默认的浏览器TVSDK广告内容解析程序或注册其自己的内容解析程序。

您还可以使用`MediaPlayerItemConfig.adTags`为默认`ManifestCuesOpportunityGenerator`类添加更多广告标记标记标记／提示，并使用`MediaPlayerItemConfig.subscribedTags`，以便TVSDK可以通知您的应用程序可能包含广告工作流程信息的其他标记。

>[!TIP]
>
>`MediaPlayerItemConfig.adTags`和`MediaPlayerItemConfig.subscribeTags`的默认值为`[MediaPlayerItemConfig.DEFAULT_AD_TAG]`。

