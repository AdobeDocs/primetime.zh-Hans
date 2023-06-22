---
description: 您可以使用TVSDK配置文件(AdobeTVSDKConfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意定义源URL转换规则。
keywords: 创意选择规则；AdobeTVSDKConfig；广告创意优先级；转换规则
title: 更新广告创意选择规则
exl-id: e364a033-7244-4de6-8505-91fb3e56959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 概述 {#update-ad-creative-selection-rules-overview}

您可以使用TVSDK配置文件(AdobeTVSDKConfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意定义源URL转换规则。

当视频播放器向广告服务器发出请求时，VAST/VMAP响应通常包括多个广告创意( `MediaFile` 元素)，每个元素都提供指向不同容器编解码器版本的URL。 在某些情况下，VAST/VMAP响应中的广告创意各自为广告提供不同的比特率。 如果要为这些广告创意指定自己的优先级和转换规则，可以在 [!DNL AdobeTVSDKConfig.json] 配置文件。

>[!IMPORTANT]
>
>* 请勿更改TVSDK配置文件的名称。 名称必须保留 [!DNL AdobeTVSDKConfig.json].
>* 您可以将此文件放在包可访问的任何位置。
>


您可以在中指定两种类型的规则 [!DNL AdobeTVSDKConfig.json]： *优先级* 规则和 *标准化* 规则。

**[!UICONTROL Disabling Pre-Roll]**

要禁用前置，您需要将默认机会生成器更改为不进行前置调用。 默认情况下，TVSDK使用以下机会生成器：

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

要在实时流上禁用前置滚动，这应该更改为仅包含SpliceOutOpportunityGenerator：

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```
