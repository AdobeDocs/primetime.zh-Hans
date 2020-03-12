---
description: TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。
seo-description: TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。
seo-title: 机会生成器和内容解析器
title: 机会生成器和内容解析器
uuid: e1d658eb-cb6c-407d-9163-2dbf62ba1d19
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 机会生成器和内容解析器{#opportunity-generators-and-content-resolvers}

机会检测器是TVSDK组件，它检测流中的自定义标记并识别放置机会。 这些机会将发送到内容解析程序，内容解析程序根据放置机会属性和元数据自定义内容／广告插入工作流。

TVSDK包含默认的机会检测器：

* `PTOpportunityResolver`，了解默认广告提示

TVSDK还包含默认内容解析程序，该解析程序根据播放器项目中的元数据键提供要插入的内容：

* `PTContentResolver`

您可以通过以下方式覆盖默认的机会检测器和内容解析器以自定义广告工作流程：

* 添加对自定义标签检测的支持
* 识别广告插入的自定义标记
* 创建自定义广告提供商
* 遮蔽内容

TVSDK提供默认的机会生成器和内容解析器，它们将广告放在时间轴中，这些生成器和解析器基于清单中的非标准标记。 您的应用程序可能需要根据清单中识别的机会（如封锁期的指示器）来更改时间轴。

A表 *`opportunity`* 示时间线上通常指示广告投放机会的兴趣点。 此机会还可以指示可能影响时间线的自定义操作，如封锁期。 An *`opportunity generator`* designs the specific opportunity(tags)in the timeline and notifications TVSDK thase opportunitys have be tagged. 在的时间轴中通过包括非标 `PTTimedMetadata` 准（非HLS）标记来识别机会。

当应用程序收到机会（标签）通知时，您的应用程序可能会通过（例如，插入一系列广告）切换到备用流（封锁期）或以其他方式编辑时间轴内容来更改时间轴。 默认情况下，TVSDK会调用相应的 *`content resolver`* 时间轴更改或操作。 您的应用程序可以使用默认的TVSDK广告内容解析程序或注册自己的内容解析程序。

您还可以使用添 `PTSDKConfig.setAdTags``PTSDKConfig.setSubscribedTags` 加更多广告标记标记标记／提示，以便TVSDK能够识别和使用您的应用程序，并通知您的应用程序可能包含广告工作流程信息的其他标记。

自定义解析程序的一个可能用途是用于封锁期。 要处理这些期间，您的应用程序可以实施并注册一个负责处理封锁标签的封锁机会检测器。 当TVSDK遇到此标记时，它将轮询所有注册内容解析器以找到处理指定标记的第一个解析器。 在此示例中，它是封锁内容解析程序，例如，它可以在标签指定的持续时间内，将播放器上的当前项目替换为替代内容。
