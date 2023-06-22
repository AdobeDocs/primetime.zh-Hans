---
description: 使用帮助程序类AuditudeSettings设置Adobe Primetime ad decisioning元数据。
title: 设置广告插入元数据
exl-id: 03b2237b-6b3b-46cf-bc0b-691513033463
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 设置广告插入元数据{#set-up-ad-insertion-metadata}

使用帮助程序类AuditudeSettings设置Adobe Primetime ad decisioning元数据。

>[!TIP]
>
>Adobe Primetime ad decisioning以前称为Auditude 。

1. 构建 `AuditudeSettings` 实例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 设置Adobe Primetime ad decisioning mediaID、zoneID、域和可选的定位参数。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 创建 `MediaResource` 使用媒体流URL和之前创建的广告元数据来创建实例。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 加载 `MediaResource` 对象通过 `MediaPlayer.replaceCurrentResource(resource)` 方法。

   此 `MediaPlayer` 开始加载和处理媒体流清单。

1. 当 `MediaPlayer` 转换为INITIALIZED状态，以a的形式获取媒体流特征 `MediaPlayerItem` 实例通过 `MediaPlayer.CurrentItem` 属性。
1. （可选）查询 `MediaPlayerItem` 实例以查看流是否处于实时状态，而不管它是否具有替代音频轨道。

   此信息可帮助您为播放准备UI。 例如，如果您知道有两个音轨，则可以包含一个UI控件来在这些音轨之间切换。

1. 调用 `MediaPlayer.prepareToPlay` 以启动广告工作流。

   解析广告并将其放到时间轴上后， `  MediaPlayer ` 转换为“已准备”状态。
1. 调用 `MediaPlayer.play` 以开始播放。
现在，浏览器TVSDK在媒体播放时包含广告。
