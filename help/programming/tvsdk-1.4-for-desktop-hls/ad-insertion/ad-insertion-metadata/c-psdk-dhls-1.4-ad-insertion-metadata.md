---
description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime广告决策)需要配置值才能启用与提供商的连接。
seo-description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime广告决策)需要配置值才能启用与提供商的连接。
seo-title: 广告插入元数据
title: 广告插入元数据
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# 广告插入元数据{#ad-insertion-metadata}

要允许广告解析程序工作，广告提供商(如Adobe Primetime广告决策)需要配置值才能启用与提供商的连接。

TVSDK包括Primetime广告决策库。 要使您的内容包含来自Primetime广告决策服务器的广告，您的应用程序必须提供以下必需的`AuditudeSettings`信息：

* `mediaID`，这是要播放的视频的唯一标识符。

   发布者在向Adobe Primetime广告决策服务器提交视频内容和广告信息时分配mediaID。 此ID由Primetime广告决策使用，从服务器检索视频的相关广告信息。

* 由Adobe分配的`zoneID`标识您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据您的需求和广告提供商的需求包含这些参数。

## 设置广告插入元数据{#set-up-ad-insertion-metadata}

使用帮助类AuditudeSettings（它扩展了MetadataNode类）设置Adobe Primetime广告决策元数据。

>[!TIP]
>
>Adobe Primetime广告决策之前被称为Auditude。

广告元数据位于`MediaResource.metadata`属性中。 开始播放新视频时，您的应用程序负责设置正确的广告元数据。

1. 构建`AuditudeSettings`实例。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime广告决策媒体ID、zoneID、域和可选定位参数。

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >媒体ID被TVSDK用作字符串，它被转换为md5值，并用于Primetime广告决策URL请求中的`u`值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 使用媒体流URL和先前创建的广告元数据创建`MediaResource`实例。

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. 通过`MediaPlayer.replaceCurrentResource`方法加载`MediaResource`对象。

   `MediaPlayer`开始加载和处理媒体流清单。

1. （可选）查询`MediaPlayerItem`实例，以查看流是否处于实时状态，而不管它是否具有替代音轨，或者流是否受保护。

   此信息可以帮助您为播放准备UI。 例如，如果您知道有两个音轨，则可以包含在这些音轨之间切换的UI控件。

1. 致电`MediaPlayer.prepareToPlay`开始广告工作流程。

   广告解析并放在时间轴上后，`MediaPlayer`过渡到PREPARED状态。
1. 调用`MediaPlayer.play`开始播放。

TVSDK现在在播放媒体时包含广告。