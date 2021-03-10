---
description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需请求，接收指定内容的广告信息，并分阶段将广告放入内容中。
title: 插入广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# 概述{#inserting-ads-overview}

广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需请求，接收指定内容的广告信息，并分阶段将广告放入内容中。

*`ad break`*&#x200B;包含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告分段的成员插入主内容中。

## 禁用前置广告{#disable-preroll-ads}

要禁用前滚，请更改默认机会生成器以不进行前滚调用。 默认的机会生成器是：

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

要禁用实时流上的预卷，请更改上面的内容，以仅包含SpliceOutOpportunityGenerator:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```
