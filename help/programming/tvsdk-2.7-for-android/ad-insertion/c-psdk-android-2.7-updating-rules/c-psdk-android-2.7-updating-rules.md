---
description: 您可以使用TVSDK配置文件(AdobeTVSDKConfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意定义源URL转换规则。
keywords: 创意选择规则；AdobeTVSDKConfig；广告创意优先级；转换规则
title: 更新广告创意选择规则
exl-id: c11a7249-0036-4859-9e98-b0cac9ade5b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 概述 {#update-ad-creative-selection-rules-overview}

您可以使用TVSDK配置文件(AdobeTVSDKConfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意定义源URL转换规则。

当视频播放器向广告服务器发出请求时，VAST/VMAP响应通常包括多个广告创意( `MediaFile` 元素)，每个元素都提供指向不同容器编解码器版本的URL。 在某些情况下，VAST/VMAP响应中的广告创意各自为广告提供不同的比特率。 如果要为这些广告创意指定自己的优先级和转换规则，可以在 [!DNL AdobeTVSDKConfig.json] 配置文件。

>[!IMPORTANT]
>
>* 请勿更改TVSDK配置文件的名称。 名称必须保留 [!DNL AdobeTVSDKConfig.json].
>* 此文件必须放在 [!DNL assets/] 文件夹中的任意位置。
>* 在广告播放时更改音轨不会更改音轨。 播放器不应允许用户在广告播放时更改音轨。
>


您可以在中指定两种类型的规则 [!DNL AdobeTVSDKConfig.json]： *优先级* 规则和 *标准化* 规则。

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

广告规则是使用JSON文件指定的。 在两个版本的TVSDK中，JSON文件的格式保持不变。 但是，在TVSDK v2.5中，必须在可通过HTTP URL访问的位置上托管Ad rules JSON文件。 该应用程序可以使用AuditudeSettings的实例：

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
