---
description: 这些类有助于在时间轴中检测放置内容（如广告）的机会。
seo-description: 这些类有助于在时间轴中检测放置内容（如广告）的机会。
seo-title: 时间轴生成器类
title: 时间轴生成器类
uuid: 1e36b738-0684-44f0-b3c3-dd656c70f705
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 时间轴生成器类{#timeline-generators-classes}

这些类有助于在时间轴中检测放置内容（如广告）的机会。

包：[com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| 名称 | 说明 |
|---|---|
| [AdSignlingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | 为指定广告信令模式创建初始机会的类。 |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | 所有机会生成器的基类。 |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | 机会生成器用来与TVSDK组件通信的接口。 |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | 类，它监视播放时间线并检测作为SpliceOut注释插入到清单中的广告放置机会。 |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | 使用定时元数据信息检测和生成广告机会的机会生成器的默认实现。 |