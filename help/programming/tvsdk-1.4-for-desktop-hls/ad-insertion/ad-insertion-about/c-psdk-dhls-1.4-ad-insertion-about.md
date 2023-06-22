---
description: 广告插入可解析以下内容的广告：视频点播(VOD) 、实时流以及带有广告跟踪和广告播放的线性流。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。
title: 插入广告
exl-id: 3a472435-2e37-46d6-8c08-dd6e953c7a7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 概述 {#inserting-ads-overview}

广告插入可解析以下内容的广告：视频点播(VOD) 、实时流以及带有广告跟踪和广告播放的线性流。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。

An *`ad break`* 包含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告时间的成员，插入主内容中。

## 禁用前置广告 {#disable-preroll-ads}

要禁用前置，请将默认机会生成器更改为不进行前置调用。 默认机会生成器是：

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

要在实时流上禁用前置滚动，请将以上内容更改为仅包含SpliceOutOpportunityGenerator：

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
