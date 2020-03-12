---
description: 使用帮助类AuditudeSettings（它扩展了MetadataNode类）设置Adobe Primetime广告决策元数据。
seo-description: 使用帮助类AuditudeSettings（它扩展了MetadataNode类）设置Adobe Primetime广告决策元数据。
seo-title: 设置广告插入元数据
title: 设置广告插入元数据
uuid: 5c807fad-4927-4547-b58c-f37e505e651c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 设置广告插入元数据 {#set-up-ad-insertion-metadata}

使用帮助类AuditudeSettings（它扩展了MetadataNode类）设置Adobe Primetime广告决策元数据。

>[!TIP]
>
>Adobe Primetime广告决策以前称为Auditude。

广告元数据位于属 `MediaResource.Metadata` 性中。 开始播放新视频时，您的应用程序负责设置正确的广告元数据。

1. 构建实 `AuditudeSettings` 例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime广告决策 `mediaID`、 `zoneID`和 `<ph conkeyref="phrases/primetime-sdk-name"/>`可选定位参数。

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >媒体ID由TVSDK使用为字符串，它被转换为md5值，并用于Primetime广告决策URL请 `u` 求中的值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 使用媒 `MediaResource` 体流URL和先前创建的广告元数据创建实例。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 通过方 `MediaResource` 法加载对 `MediaPlayer.replaceCurrentResource` 象。

   开始 `MediaPlayer` 加载和处理媒体流清单。

1. 当转换 `MediaPlayer` 到“已初始化”状态时，通过该方法以实例的形式获得媒 `MediaPlayerItem` 体流特 `MediaPlayer.CurrentItem` 性。
1. （可选）查询实 `MediaPlayerItem` 例以查看流是否处于实时状态，而不管它是具有替代音轨还是流受保护。

   此信息可以帮助您准备播放的UI。 例如，如果您知道有两个音轨，则可以包含在这些音轨之间切换的UI控件。

1. 致电 `MediaPlayer.prepareToPlay` 启动广告工作流程。

   在广告解析并放在时间轴上后，将转 `MediaPlayer` 换到状 `PREPARED` 态。
1. 调 `MediaPlayer.play` 用以开始播放。

TVSDK现在在播放媒体时包含广告。