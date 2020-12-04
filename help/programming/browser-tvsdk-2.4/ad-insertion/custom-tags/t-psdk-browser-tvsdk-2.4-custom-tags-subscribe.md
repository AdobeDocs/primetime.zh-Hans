---
description: 浏览器TVSDK在媒体演示文稿描述(MPD)文件中每次遇到订阅标记时，都会为这些对象准备TimedMetadata对象。
seo-description: 浏览器TVSDK在媒体演示文稿描述(MPD)文件中每次遇到订阅标记时，都会为这些对象准备TimedMetadata对象。
seo-title: 订阅自定义广告标记
title: 订阅自定义广告标记
uuid: 208f61f4-dc33-4363-aa71-878458740a8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# 订阅自定义广告标记{#subscribe-to-custom-ad-tags}

浏览器TVSDK在媒体演示文稿描述(MPD)文件中每次遇到订阅标记时，都会为这些对象准备TimedMetadata对象。

在播放开始之前，必须订阅标记。
要订阅标记，请将包含自定义标记名称的矢量设置为`subscribedTags`属性。 如果还需要更改默认机会生成器使用的广告标记，请将包含自定义广告标记名称的矢量设置为`adTags`属性。

要订阅自定义标记：

1. 创建新的媒体播放器项配置。

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
   >如果您处理的是HLS流，请记住包含`#`前缀。

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 将更新的矢量指定到`mediaPlayerItemConfig.subscribeTags`属性。

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

1. 将更新的矢量指定到`mediaPlayerItemConfig.adTags`属性。

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 加载媒体流时，请使用媒体播放器项配置。

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

