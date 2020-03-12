---
description: 这些类为广告、命名空间和跟踪提供元数据。
seo-description: 这些类为广告、命名空间和跟踪提供元数据。
seo-title: 元数据类
title: 元数据类
uuid: e3884825-132c-4c5c-bc58-00c2967d9fa8
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 元数据类 {#metadata-classes}

这些类为广告、命名空间和跟踪提供元数据。

包： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| 名称 | 说明 |
|---|---|
| [AdSignalingMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | 公开短语中支持的信令模式的枚举类。 |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 专门为短语 `Metadata` 扩展的类。 提供要配置的属性以解析给定媒体项目的短语广告。 您必须设置所有必需的属性（包括区域ID、媒体ID和广告服务器URL）才能配置播放器以成功解析广告。 |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | 已弃用。 使用 `Metadata`。 |
| [DefaultMetadataKeys](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | 课程。 |
| [元数据](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定义用于配置播放器和其他对象的所有可用元数据的通用界面。 |
| [元数据节点](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 已弃用。 使用 `Metadata`。 |
| [MetadataUtils](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | 用于处理元数据的方法类。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒体流中的定时元数据的原始表示形式的类。 |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | 包含定时元数据（在播放列表或流中）支持的类型的类，如ID3元数据或标记。 |