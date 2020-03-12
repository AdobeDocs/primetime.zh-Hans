---
description: 您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: 您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。
seo-title: 更新广告创意选择规则
title: 更新广告创意选择规则
uuid: fddc5593-db40-4b03-bd7e-4b5fe5b6f650
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 概述 {#update-ad-creative-selection-rules-overview}

您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。

当视频播放器向广告服务器发出请求时，VAST/VMAP响应通常包括多个广告创意（元素），每个元素都提供指向不同容器编解码器版本的URL。 `MediaFile` 在某些情况下，VAST/VMAP响应中的广告创意人员为广告提供不同的比特率。 如果要为这些广告创意人员指定自己的优先级和转换规则，可以在配置文件中 [!DNL AdobeTVSDKConfig.json] 指定。

>[!IMPORTANT]
>
>* 请勿更改TVSDK配置文件的名称。 名称必须保留 [!DNL AdobeTVSDKConfig.json]。
>* 此文件必须放在项目 [!DNL assets/] 的文件夹中。
>* 在播放广告时更改音轨不会更改音轨。 播放广告时，播放器不应允许用户更改音轨。
>



您可以在中指定两种类型的规则 [!DNL AdobeTVSDKConfig.json]:优 *先级规则* 和标准 *化规则* 。

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

广告规则是使用JSON文件指定的。 TVSDK的两个版本中的JSON文件格式保持不变。 但是，在TVSDK v2.5中，广告规则JSON文件必须托管在可通过HTTP URL访问的位置。 应用程序可以使用AuditudeSettings的实例：

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```

