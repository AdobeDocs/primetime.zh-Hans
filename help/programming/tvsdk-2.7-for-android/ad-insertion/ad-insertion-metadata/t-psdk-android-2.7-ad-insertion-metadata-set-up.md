---
description: 使用帮助程序类AuditudeSettings（用于扩展MetadataNode类）来设置Adobe Primetime ad decisioning元数据。
title: 设置广告插入元数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 设置广告插入元数据 {#set-up-ad-insertion-metadata}

使用帮助程序类AuditudeSettings（用于扩展MetadataNode类）来设置Adobe Primetime ad decisioning元数据。

>[!TIP]
>
>Adobe Primetime ad decisioning以前称为Auditude。

广告元数据位于 `MediaResource.Metadata` 属性。 开始播放新视频时，您的应用程序负责设置正确的广告元数据。

1. 构建 `AuditudeSettings` 实例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime广告决策 `mediaID`， `zoneID`， `<ph conkeyref="phrases/primetime-sdk-name"/>`和可选的定位参数。

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
   >媒体ID由TVSDK作为字符串使用，将转换为md5值，用于 `u` Primetime广告决策URL请求中的值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 创建 `MediaResource` 使用媒体流URL和之前创建的广告元数据执行实例。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 加载 `MediaResource` 对象通过 `MediaPlayer.replaceCurrentResource` 方法。

   此 `MediaPlayer` 开始加载和处理媒体流清单。

1. 当 `MediaPlayer` 转换为INITIALIZED状态，以a形式获取媒体流特性 `MediaPlayerItem` 实例通过 `MediaPlayer.CurrentItem` 方法。
1. （可选）查询 `MediaPlayerItem` 实例以了解流是否为实时流，无论它是否具有替代音频轨道或流是否受保护。

   此信息可帮助您为播放准备UI。 例如，如果您知道有两个音轨，则可以包含可在两个音轨之间切换的UI控件。

1. 调用 `MediaPlayer.prepareToPlay` 以启动广告工作流。

   解析广告并将其放到时间轴上后， `MediaPlayer` 过渡到 `PREPARED` 省/州。
1. 调用 `MediaPlayer.play` 以开始播放。

现在，TVSDK会在您的媒体播放时包含广告。
