---
description: 这些类为广告、命名空间和跟踪提供元数据。
title: 元数据类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 元数据类{#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

| **名称** | **说明** |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | 类，它提供应配置用于解析给定媒体项的广告的属性。 必须设置所有必需属性才能配置播放器以成功解析广告。 |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | 专门用于Adobe Primetime广告决策的`PTAdMetadata`扩展的类。 提供要配置的属性，用于解决给定媒体项目的Adobe Primetime广告决策广告。 您必须设置所有必需属性，包括区域ID、媒体ID和广告服务器URL，才能配置播放器以成功解析广告。 |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | 定义基类，用于为播放器和其他对象配置所有可用元数据。 |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | 表示流中的自定义HLS标记的类。 |
| [PTTrakingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | 为所有跟踪和分析相关元数据定义基类。 |