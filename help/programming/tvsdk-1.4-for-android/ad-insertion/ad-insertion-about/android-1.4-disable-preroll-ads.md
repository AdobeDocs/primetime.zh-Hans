---
title: 禁用前置广告
description: 禁用前置广告
copied-description: true
exl-id: ff52588e-540e-4072-bec0-e531c8cb6fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---

# 禁用前置广告{#disable-pre-roll-ads}

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
