---
description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。
title: 广告插入元数据
exl-id: 83c0fd25-dbc3-4529-b81a-16ff78012c80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 广告插入元数据 {#ad-insertion-metadata}

要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。

TVSDK包括Primetime广告决策库。 要使您的内容包含来自Primetime Ad Decisioning服务器的广告，您的应用程序必须提供以下必需信息 `AuditudeSettings` 信息：

* `mediaID`，这是要播放的视频的唯一标识符。

   在将视频内容和广告信息提交到Adobe Primetime广告决策服务器时，发布者会分配mediaID。 Primetime广告决策使用此ID从服务器检索视频的相关广告信息。

* 您的 `zoneID`由Adobe分配，用于标识您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据自己的需求和广告提供商的需求来包含这些参数。

## 设置广告插入元数据 {#set-up-ad-insertion-metadata}

使用帮助程序类AuditudeSettings （扩展MetadataNode类）来设置Adobe Primetime ad decisioning元数据。

>[!TIP]
>
>Adobe Primetime ad decisioning以前称为Auditude。

广告元数据位于 `MediaResource.metadata` 属性。 开始播放新视频时，您的应用程序负责设置正确的广告元数据。

1. 构建 `AuditudeSettings` 实例。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime ad decisioning mediaID、zoneID、域和可选的定位参数。

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
   >媒体ID由TVSDK作为字符串使用，将转换为md5值，并用于 `u` Primetime广告决策URL请求中的值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 创建 `MediaResource` 使用媒体流URL和之前创建的广告元数据来创建实例。

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. 加载 `MediaResource` 对象通过 `MediaPlayer.replaceCurrentResource` 方法。

   此 `MediaPlayer` 开始加载和处理媒体流清单。

1. （可选）查询 `MediaPlayerItem` 实例以查看流是否处于实时状态，无论它是否有替代音频轨道，或者流是否受到保护。

   此信息可帮助您为播放准备UI。 例如，如果您知道有两个音轨，则可以包含一个UI控件来在这些音轨之间切换。

1. 调用 `MediaPlayer.prepareToPlay` 以启动广告工作流。

   解析广告并将其放到时间轴上后， `MediaPlayer` 转换为“已准备”状态。
1. 调用 `MediaPlayer.play` 以开始播放。

现在，TVSDK在媒体播放时包含广告。
