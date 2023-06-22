---
description: 这些类为广告、命名空间和跟踪提供元数据。
title: 元数据类
exl-id: 4014b496-7fc4-4fa9-98da-28350668d35f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 元数据类 {#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

包： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| 名称 | 描述 |
|---|---|
| [AdSignalingMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | 枚举类公开短语中支持的信令模式。 |
| [Auditudesettings](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 扩展的类 `Metadata` 专门针对短语。 提供为解析给定媒体项目的短语广告而配置的属性。 您必须设置所有必需的属性（包括区域ID、媒体ID和广告服务器URL），以配置播放器以便成功解析广告。 |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | 已弃用。 使用 `Metadata`. |
| [DefaultMetadataKey](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | 班级。 |
| [元数据](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定义用于为播放器和其他对象配置所有可用元数据的通用接口。 |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 已弃用。 使用 `Metadata`. |
| [Metadatautils](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | 使用元数据的方法类。 |
| [Timedatadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒体流中的定时元数据的原始表示法的类。 |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | 包含定时元数据（在播放列表或流中）所支持类型（如ID3元数据或标记）的类。 |
