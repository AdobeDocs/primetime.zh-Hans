---
description: 浏览器TVSDK在媒体演示文稿描述(MPD)文件中每次遇到订阅标记时，都会为这些对象准备TimedMetadata对象。
title: 订阅自定义广告标记
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 订阅自定义广告标签{#subscribe-to-custom-ad-tags}

浏览器TVSDK在媒体演示文稿描述(MPD)文件中每次遇到订阅标记时，都会为这些对象准备TimedMetadata对象。

在播放开始之前，必须订阅标记。
要订阅标记，请将包含自定义标记名称的矢量设置为`subscribedTags`属性。 如果您还需要更改默认业务机会生成器使用的广告标签，请将包含自定义广告标签名称的矢量设置为`adTags`属性。

要订阅自定义标记，请执行以下操作：

1. 创建新的媒体播放器项配置。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 创建一个空字符串矢量。

   ```js
   var subscribeTags = [];
   ```

1. 将自定义标记名称添加到此矢量。

   >[!IMPORTANT]
   >
   >如果您正在处理HLS流，请记住包含`#`前缀。

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 将更新的矢量分配给`mediaPlayerItemConfig.subscribeTags`属性。

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 创建一个空字符串矢量。

   ```js
   var adTags= [];
   ```

1. 将自定义广告标记名称添加到此矢量。

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 将更新的矢量分配给`mediaPlayerItemConfig.adTags`属性。

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 在加载媒体流时使用媒体播放器项配置。

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

