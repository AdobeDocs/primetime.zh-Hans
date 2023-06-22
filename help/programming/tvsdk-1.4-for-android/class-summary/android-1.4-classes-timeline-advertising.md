---
description: 这些类提供有关时间轴内发生的广告的信息。
title: 时间轴广告类
exl-id: fb31a235-6578-4da1-b732-713a2f9b24be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 时间轴广告类{#timeline-advertising-classes}

这些类提供有关时间轴内发生的广告的信息。

包： [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

包： [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| 名称 | 描述 |
|--- |--- |
| [广告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定义广告抽象并保存所有广告信息的类。 它由唯一ID、持续时间和 `MediaResource`. 此 `MediaResource` 包含实际广告内容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要显示的资源的类。 表示广告资源的类。 |
| [广告时间](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 类可统一查看将在播放过程中的某个时间点播放的多个广告。 |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | 广告时间放置操作类。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | 定义与搜索时绕过广告的用户相关的广告播放策略的枚举。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示与资产关联的点击实例的类。 此实例包含有关点进URL和标题的信息，可用于向用户提供其他信息。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | 定义AdPolicySelector API调用的属性的接口。 这些属性提供了用于实施每个广告行为的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | 用于实施广告行为的广告策略选择器界面。 应用程序可以通过实现所有必需的方法或通过扩展现有的默认策略选择器类来自定义特定行为，来符合此接口。 |
| `auditude.AuditudeAdProvider` | 已弃用。 使用AuditudeResolver。 |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | 在短语处理中处理primetime和解析的类。 |
| [Auditudetracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | 实现ContentTracker接口并定义Primetime广告跟踪事件的类。 |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | 处理短语处理中的广告解析部分的类。 |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | 定义在以下情况下必须实施的协议的接口：要创建旨在与库或自定义广告跟踪器集成的广告跟踪模块。 此界面要求您定义向远程广告跟踪系统报告广告进度事件的方式。 |
| [投放位置信息](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | 抽象放置信息请求的类。 每个已解析广告必须附加一个版面信息。 投放位置信息描述广告在时间轴上的放置位置。 它包含如下信息： <ul><li>投放位置（以毫秒为单位） </li><li>投放类型（前置、中置或后置） </li><li>即将替换的主内容块的持续时间</li></ul> |
