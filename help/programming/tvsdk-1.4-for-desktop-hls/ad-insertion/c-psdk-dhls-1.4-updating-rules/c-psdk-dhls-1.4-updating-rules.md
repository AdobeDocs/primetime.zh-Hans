---
description: 您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。
seo-description: 您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。
seo-title: 更新广告创意选择规则
title: 更新广告创意选择规则
uuid: 9eb4ccc2-425f-4c01-a095-f2043df4e25c
translation-type: tm+mt
source-git-commit: 6837c753b2f031b024ff510cda670340f346c4e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# 概述{#updating-ad-creative-selection-rules}

您可以使用TVSDK配置文件(AdobeTVSDKonfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意人员定义源URL转换规则。

当视频播放器向广告服务器发出请求时，VAST/VMAP响应通常包括多个广告创意（`MediaFile`元素），每个元素都提供指向不同容器编解码器版本的URL。 在某些情况下，VAST/VMAP响应中的广告创意人员为广告提供不同的比特率。 如果要为这些广告创意指定自己的优先级和转换规则，可以在[!DNL AdobeTVSDKConfig.json]配置文件中指定。

>[!IMPORTANT]
>
>* 请勿更改TVSDK配置文件的名称。 名称必须保留[!DNL AdobeTVSDKConfig.json]。
>* 此文件应托管在您的内容投放网络(CDN)上。

>



可以在[!DNL AdobeTVSDKConfig.json]中指定两种类型的规则：*优先级*&#x200B;规则和&#x200B;*标准化*&#x200B;规则。
