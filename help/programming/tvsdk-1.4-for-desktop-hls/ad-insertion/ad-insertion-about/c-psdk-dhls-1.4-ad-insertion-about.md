---
description: 广告插入可解析用于视频点播(VOD) 、实时流以及具有广告跟踪和广告播放的线性流的广告。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。
title: 插入广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 概述 {#inserting-ads-overview}

广告插入可解析用于视频点播(VOD) 、实时流以及具有广告跟踪和广告播放的线性流的广告。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。

An *`ad break`* 包含一个或多个按顺序播放的广告。 TVSDK会将广告作为一个或多个广告时间的成员，插入主内容中。

## 禁用前置广告 {#disable-preroll-ads}

要禁用前置，请将默认机会生成器更改为不进行前置调用。 默认的opportunity生成器为：

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

要在实时流上禁用前置滚动，请更改上述内容以仅包含SpliceOutOpportunityGenerator：

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
