---
description: 这些类提供有关时间轴内发生的广告的信息。
title: 时间轴广告类
exl-id: 2ac1f6b7-48b2-4d9c-b39d-a7e6f1ff2ac5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 时间轴广告类 {#timeline-advertising-classes}

这些类提供有关时间轴内发生的广告的信息。

包： [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
包： [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| 名称 | 描述 |
|---|---|
| [广告](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 定义广告抽象并保存所有广告信息的类。 它由唯一ID、持续时间和 `MediaResource`. 此 `MediaResource` 包含实际广告内容所在的URL。 |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 表示要显示的资源的类。 表示广告资源的类。 |
| [广告时间](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 类可统一查看将在播放过程中的某个时间点播放的多个广告。 |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | 定义与搜索时绕过广告的用户相关的广告播放策略的枚举。 |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | 与特定广告时间关联的时间线项目。 |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | 有关何时将广告时间标记为已观看的可能策略的枚举类。 |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 表示与资产关联的点击实例的类。 此实例包含有关点进URL和标题的信息，可用于向用户提供其他信息。 |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | 有关在搜寻或特技播放模式后从何处继续播放广告时间的可能策略的枚举类。 |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | 列举类，列出播放器的播放方式，例如搜寻或正常播放。 |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 定义属性的接口 `AdPolicySelector` API调用。 这些属性提供了用于实施每个广告行为的上下文。 |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 用于实施广告行为的广告策略选择器界面。 应用程序可以通过实现所有必需的方法或通过扩展现有的默认策略选择器类来自定义特定行为，来符合此接口。 |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | 与特定广告关联的时间线项目。 |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | 在TVSDK进程中处理primetime和解析的类。 |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | TVSDK支持的所有广告类型的枚举。 |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | 班级。 |
