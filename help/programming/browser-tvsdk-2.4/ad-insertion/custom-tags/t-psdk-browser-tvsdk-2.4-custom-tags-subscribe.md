---
description: 每次在媒体演示说明(MPD)文件中遇到订阅的标记时，浏览器TVSDK都会为这些对象准备TimedMetadata对象。
title: 订阅自定义广告标记
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 订阅自定义广告标记{#subscribe-to-custom-ad-tags}

每次在媒体演示说明(MPD)文件中遇到订阅的标记时，浏览器TVSDK都会为这些对象准备TimedMetadata对象。

在开始播放之前，必须订阅标记。
要订阅标记，请将包含自定义标记名称的矢量设置为 `subscribedTags` 属性。 如果您还需要更改默认机会生成器使用的广告标记，请将包含自定义广告标记名称的矢量设置为 `adTags` 属性。

要订阅自定义标记，请执行以下操作：

1. 创建新的媒体播放器项目配置。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 创建空字符串矢量。

   ```js
   var subscribeTags = [];
   ```

1. 将自定义标记名称添加到此矢量。

   >[!IMPORTANT]
   >
   >如果您要处理HLS流，请记住包含 `#` 前缀。

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 将更新的矢量分配给 `mediaPlayerItemConfig.subscribeTags` 属性。

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 创建空字符串矢量。

   ```js
   var adTags= [];
   ```

1. 将自定义广告标记名称添加到此矢量。

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 将更新的矢量分配给 `mediaPlayerItemConfig.adTags` 属性。

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 加载媒体流时，请使用媒体播放器项目配置。

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
