---
description: 您可以使用TVSDK配置文件(AdobeTVSDKConfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意定义源URL转换规则。
title: 更新广告创意选择规则
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 概述 {#updating-ad-creative-selection-rules}

您可以使用TVSDK配置文件(AdobeTVSDKConfig.json)更新VAST/VMAP响应上广告创意选择的优先级。 您还可以使用此配置文件为广告创意定义源URL转换规则。

当视频播放器向广告服务器发出请求时，VAST/VMAP响应通常包括多个广告创意( `MediaFile` 元素)，每个元素都提供指向不同容器编解码器版本的URL。 在某些情况下，VAST/VMAP响应中的广告创意各自为广告提供不同的比特率。 如果要为这些广告创意指定自己的优先级和转换规则，可以在 [!DNL AdobeTVSDKConfig.json] 配置文件。

>[!IMPORTANT]
>
>* 请勿更改TVSDK配置文件的名称。 名称必须保留 [!DNL AdobeTVSDKConfig.json].
>* 此文件应托管在您的内容交付网络(CDN)上。
>


您可以在中指定两种类型的规则 [!DNL AdobeTVSDKConfig.json]： *优先级* 规则和 *标准化* 规则。
