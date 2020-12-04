---
description: 您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: 您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。
seo-title: 更新广告创意选择规则
title: 更新广告创意选择规则
uuid: c33fe1f0-78cb-4dc2-89d2-e9fb1bf0e73f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# 概述{#update-ad-creative-selection-rules-overview}

您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。

当视频播放器向广告服务器发出请求时，VAST/VMAP响应通常包括多个广告创意（`MediaFile`元素），每个元素都提供指向不同容器编解码器版本的URL。 在某些情况下，VAST/VMAP响应中的广告创意人员为广告提供不同的比特率。 如果要为这些广告创意指定自己的优先级和转换规则，可以在[!DNL AdobeTVSDKConfig.json]配置文件中指定。

>[!IMPORTANT]
>
>* 请勿更改TVSDK配置文件的名称。 名称必须保留[!DNL AdobeTVSDKConfig.json]。
>* 您可以将此文件放在捆绑包可以访问的任何地方。

>



可以在[!DNL AdobeTVSDKConfig.json]中指定两种类型的规则：*优先级*&#x200B;规则和&#x200B;*标准化*&#x200B;规则。

**[!UICONTROL Disabling Pre-Roll]**

要禁用前置调用，您需要更改默认的机会生成器，以便不进行前置调用。 默认情况下，TVSDK使用以下机会生成器：

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

要禁用实时流上的预卷，应将其更改为仅包含SpliceOutOpportunityGenerator:

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

