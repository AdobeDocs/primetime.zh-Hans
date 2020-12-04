---
description: 这些类提供有关时间轴内发生的广告的信息。
seo-description: 这些类提供有关时间轴内发生的广告的信息。
seo-title: 时间轴广告课程
title: 时间轴广告课程
uuid: f424fa13-778b-458d-bc82-389441a8a56a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# 时间轴广告类{#timeline-advertising-classes}

这些类提供有关时间轴内发生的广告的信息。

包：[com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
包：[com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| 名称 | 说明 |
|---|---|
| [广告](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定义广告抽象并包含所有广告信息的类。 它由唯一ID、持续时间和`MediaResource`定义。 `MediaResource`包含实际广告内容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要显示的资产的类。 表示广告资产的类。 |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 对在播放过程中某个时刻将播放的多个广告提供统一视图的类。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | 定义与用户在搜索时跳过广告相关的广告播放策略的明细列表。 |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | 与特定广告中断关联的时间轴项目。 |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | 明细列表类，以了解有关何时将广告中断标记为已观看的可能策略。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示与资产关联的单击实例的类。 此实例包含有关点进URL和标题的信息，这些信息可用于向用户提供其他信息。 |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | 明细列表类，用于在搜索或技巧播放模式后在何处继续播放广告中断的可能策略。 |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | 明细列表类，它列表玩家正在玩的方式，如搜索或正常玩。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 定义`AdPolicySelector` API调用属性的接口。 这些属性提供用于强制实施每个广告行为的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 用于实施广告行为的广告策略选择器界面。 应用程序可以通过实现所有必需的方法或通过扩展现有的默认策略选择器类来自定义特定行为来符合此接口。 |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | 与特定广告关联的时间轴项目。 |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | 在TVSDK流程中处理黄金时段广告解析的类。 |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | 明细列表TVSDK支持的所有广告类型。 |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | 课。 |

