---
description: 使用帮助类AuditudeSettings设置Adobe Primetime广告决策元数据。
seo-description: 使用帮助类AuditudeSettings设置Adobe Primetime广告决策元数据。
seo-title: 设置广告插入元数据
title: 设置广告插入元数据
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 设置广告插入元数据{#set-up-ad-insertion-metadata}

使用帮助类AuditudeSettings设置Adobe Primetime广告决策元数据。

>[!TIP]
>
>Adobe Primetime广告决策之前称为Auditude。

1. 构建实 `AuditudeSettings` 例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime广告决策媒体ID、zoneID、域和可选定位参数。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 使用媒 `MediaResource` 体流URL和先前创建的广告元数据创建实例。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 通过方 `MediaResource` 法加载对 `MediaPlayer.replaceCurrentResource(resource)` 象。

   开始 `MediaPlayer` 加载和处理媒体流清单。

1. 当转换 `MediaPlayer` 到“已初始化”状态时，通过属性以实例的形式获得媒体 `MediaPlayerItem` 流特 `MediaPlayer.CurrentItem` 性。
1. （可选）查询实 `MediaPlayerItem` 例以查看流是否处于实时状态，而不管它是否具有替代音轨。

   此信息可以帮助您准备播放的UI。 例如，如果您知道有两个音轨，则可以包含在这些音轨之间切换的UI控件。

1. 致电 `MediaPlayer.prepareToPlay` 启动广告工作流程。

   在解析广告并将其放置到时间轴上后，广告将转 `  MediaPlayer ` 换到“准备”状态。
1. 调 `MediaPlayer.play` 用以开始播放。
浏览器TVSDK现在在播放媒体时包含广告。
