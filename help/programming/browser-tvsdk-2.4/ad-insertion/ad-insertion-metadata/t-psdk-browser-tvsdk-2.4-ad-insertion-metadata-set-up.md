---
description: 使用帮助程序类AuditudeSettings设置Adobe Primetime广告决策元数据。
title: 设置广告插入元数据
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 设置广告插入元数据{#set-up-ad-insertion-metadata}

使用帮助程序类AuditudeSettings设置Adobe Primetime广告决策元数据。

>[!TIP]
>
>Adobe Primetime广告决策之前称为Auditude。

1. 构建`AuditudeSettings`实例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime广告决策媒体ID、zoneID、domain和可选定位参数。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 使用媒体流URL和之前创建的广告元数据创建`MediaResource`实例。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 通过`MediaPlayer.replaceCurrentResource(resource)`方法加载`MediaResource`对象。

   `MediaPlayer`开始加载和处理媒体流清单。

1. 当`MediaPlayer`过渡为INITIALIZED状态时，通过`MediaPlayer.CurrentItem`属性以`MediaPlayerItem`实例的形式获取媒体流特性。
1. （可选）查询`MediaPlayerItem`实例以查看流是否是实时的，而不管它是否具有替代音轨。

   此信息可帮助您为播放准备UI。 例如，如果您知道有两个音轨，则可以包含在这些音轨之间切换的UI控件。

1. 致电`MediaPlayer.prepareToPlay`开始广告工作流程。

   在解析广告并将其放置到时间轴上后，`  MediaPlayer `过渡到PREPARED状态。
1. 调用`MediaPlayer.play`以开始播放。
浏览器TVSDK现在在播放媒体时包含广告。
