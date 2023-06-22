---
description: 这些类为广告、命名空间和跟踪提供元数据。
title: 元数据类
exl-id: cd4f96d1-d8ee-4008-b35f-60b797a34b85
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 元数据类 {#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

| **名称** | **描述** |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | 提供属性的类，对于给定的媒体项目，应配置这些属性以解析广告。 必须设置所有必需的属性，才能配置播放器以成功解析广告。 |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | 扩展的类 `PTAdMetadata` 专门用于Adobe Primetime ad decisioning。 提供要配置的属性，用于解析给定媒体项目的Adobe Primetime广告决策广告。 您必须设置所有必需的属性（包括区域ID、媒体ID和广告服务器URL），以配置播放器以便成功解析广告。 |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | 定义用于为播放器和其他对象配置所有可用元数据的基类。 |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | 表示流中的自定义HLS标记的类。 |
| [PTTrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | 为所有与跟踪和分析相关的元数据定义基类。 |
