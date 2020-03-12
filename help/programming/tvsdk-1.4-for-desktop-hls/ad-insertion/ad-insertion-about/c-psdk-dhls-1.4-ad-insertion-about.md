---
description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需的请求，接收有关指定内容的广告的信息，并将广告分阶段放入内容中。
seo-description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需的请求，接收有关指定内容的广告的信息，并将广告分阶段放入内容中。
seo-title: 插入广告
title: 插入广告
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概述 {#inserting-ads-overview}

广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需的请求，接收有关指定内容的广告的信息，并将广告分阶段放入内容中。

An包 *`ad break`* 含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告分段的成员插入主内容中。

## 禁用前置广告 {#disable-preroll-ads}

要禁用前置调用，请更改默认的业务机会生成器以不进行前置调用。 默认的业务机会生成器是：

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
