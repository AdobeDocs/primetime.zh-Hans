---
description: 这些类为广告、命名空间和跟踪提供元数据。
title: 元数据类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# 元数据类{#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

包：[com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 名称 | 说明 |
|---|---|
| [广告元数据](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 类，它提供应配置用于解析给定媒体项的广告的属性。 必须设置所有必需属性才能配置播放器以成功解析广告。 |
| AuditudeMetadata | 已弃用。 使用AuditudeSettings。 |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 专门用于Phrase的Java `AdvertisingMetadata`扩展的类。 提供要配置的属性，用于解析给定媒体项目的短语广告。 您必须设置所有必需属性，包括区域ID、媒体ID和广告服务器URL，才能配置播放器以成功解析广告。 |
| [元数据](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定义用于配置播放器和其他对象的所有可用元数据的通用界面。 |
| [元数据节点](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 用于存储任意键值对的通用数据结构类。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒体流中的定时元数据的原始表示的类。 |