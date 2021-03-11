---
description: 使用帮助类AuditudeSettings（它扩展了MetadataNode类）设置Adobe Primetime和决策元数据。
title: 设置广告插入元数据
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# 设置广告插入元数据{#set-up-ad-insertion-metadata}

使用帮助类AuditudeSettings（它扩展了MetadataNode类）设置Adobe Primetime和决策元数据。

>[!TIP]
>
>Adobe Primetime广告决策之前称为Auditude。

广告元数据位于`MediaResource.Metadata`属性中。 开始播放新视频时，您的应用程序负责设置正确的广告元数据。

1. 构建`AuditudeSettings`实例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime广告决策`mediaID`、`zoneID`、`domain`和可选定位参数。

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
   >媒体ID由TVSDK使用为字符串，它被转换为md5值，并用于Primetime广告决策URL请求中的`u`值。 例如：
   >
   >
   ```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. 使用媒体流URL和之前创建的广告元数据创建`MediaResource`实例。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 通过`MediaPlayer.replaceCurrentResource`方法加载`MediaResource`对象。

   `MediaPlayer`开始加载和处理媒体流清单。

1. 当`MediaPlayer`过渡到`INITIALIZED`状态时，通过`MediaPlayer.CurrentItem`方法以`MediaPlayerItem`实例的形式获取媒体流特性。
1. （可选）查询`MediaPlayerItem`实例以查看流是否是实时的，而不管它是否具有替代音轨，或者流是否受到保护。

   此信息可帮助您为播放准备UI。 例如，如果您知道有两个音轨，则可以包含在这些音轨之间切换的UI控件。

1. 致电`MediaPlayer.prepareToPlay`开始广告工作流程。

   在解析广告并将其放置到时间轴上后，`MediaPlayer`过渡到`PREPARED`状态。
1. 调用`MediaPlayer.play`以开始播放。

TVSDK现在在播放您的媒体时包含广告。
