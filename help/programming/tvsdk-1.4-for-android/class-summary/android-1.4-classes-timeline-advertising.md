---
description: 这些类提供有关时间轴内发生的广告的信息。
title: 时间轴广告课程
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# 时间轴广告类{#timeline-advertising-classes}

这些类提供有关时间轴内发生的广告的信息。

包：[com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

包：[com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| 名称 | 说明 |
|--- |--- |
| [广告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定义广告抽象并包含所有广告信息的类。 它由唯一ID、持续时间和`MediaResource`定义。 `MediaResource`包含实际广告内容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要显示的资产的类。 表示广告资产的类。 |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 在播放过程中某个点将播放的多个广告上提供统一视图的类。 |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | 广告中断放置操作类。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | 定义与用户在搜索时跳过广告相关的广告播放策略的明细列表。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示与资产关联的单击实例的类。 此实例包含有关点进URL和标题的信息，这些信息可用于向用户提供其他信息。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | 定义AdPolicySelector API调用属性的接口。 这些属性提供了用于强制实施每个广告行为的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | 用于实施广告行为的广告策略选择器界面。 通过实现所有所需的方法或通过扩展现有的默认策略选择器类来自定义特定行为，应用程序可以符合此接口。 |
| `auditude.AuditudeAdProvider` | 已弃用。 使用AuditudeResolver。 |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | 在短语流程中处理黄金时段广告解析的类。 |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | 实现ContentTracker接口并定义Primetime广告跟踪事件的类。 |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | 处理短语流程中广告解析部分的类。 |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | 定义要创建与库或自定义广告跟踪器集成的广告跟踪模块时必须实现的协议的接口。 此接口要求您定义向远程广告跟踪系统报告广告进度事件的方式。 |
| [放置信息](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | 抽象版面信息请求的类。 每个已解析的广告都必须附加一个位置信息。 版面信息描述广告在时间轴上的放置位置。 它包含以下信息： <ul><li>位置（毫秒） </li><li>放置的类型（前滚、中滚或后滚） </li><li>将要替换的主内容块的持续时间</li></ul> |
