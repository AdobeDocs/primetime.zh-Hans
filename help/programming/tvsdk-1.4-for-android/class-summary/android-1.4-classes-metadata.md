---
description: 这些类为广告、命名空间和跟踪提供元数据。
seo-description: 这些类为广告、命名空间和跟踪提供元数据。
seo-title: 元数据类
title: 元数据类
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 元数据类{#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

包： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 名称 | 说明 |
|---|---|
| [广告元数据](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 提供应配置用于解析给定媒体项目广告的属性的类。 必须设置所有必需的属性才能配置播放器以成功解析广告。 |
| AuditudeMetadata | 已弃用。 使用AuditudeSettings。 |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 专门为短语扩展Java `AdvertisingMetadata` 的类。 提供要配置的属性以解析给定媒体项目的短语广告。 您必须设置所有必需的属性（包括区域ID、媒体ID和广告服务器URL）才能配置播放器以成功解析广告。 |
| [元数据](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定义用于配置播放器和其他对象的所有可用元数据的通用界面。 |
| [元数据节点](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 用于存储任意键值对的类似数据结构的通用类。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒体流中的定时元数据的原始表示形式的类。 |