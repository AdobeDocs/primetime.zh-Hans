---
description: 这些类为广告、命名空间和跟踪提供元数据。
title: 元数据类
exl-id: 3d98c5e1-6792-419b-9638-f156f1eafd1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 元数据类{#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

包： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 名称 | 描述 |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 提供属性的类，对于给定的媒体项目，应配置这些属性以解析广告。 必须设置所有必需的属性，才能配置播放器以成功解析广告。 |
| AuditudeMetadata | 已弃用。 使用Auditudesettings。 |
| [Auditudesettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 扩展Java的类 `AdvertisingMetadata` 专门针对短语。 提供为解析给定媒体项目的短语广告而配置的属性。 您必须设置所有必需的属性（包括区域ID、媒体ID和广告服务器URL），以配置播放器以便成功解析广告。 |
| [元数据](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定义用于为播放器和其他对象配置所有可用元数据的通用接口。 |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 用于存储任意键值对的类数据结构的通用类。 |
| [Timedatadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒体流中的定时元数据的原始表示法的类。 |
