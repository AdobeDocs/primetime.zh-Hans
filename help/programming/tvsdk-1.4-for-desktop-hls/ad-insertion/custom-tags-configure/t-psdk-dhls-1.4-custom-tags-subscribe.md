---
description: 每次在内容清单中遇到订阅标记的对象时，TVSDK都会为这些对象准备TimedMetadata对象。
title: 订阅自定义标记
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记的对象时，TVSDK都会为这些对象准备TimedMetadata对象。

在开始播放之前，您必须订阅标记。
要订阅标记，请将包含自定义标记名称的矢量分配给 `subscribedTags` 属性。 如果您还需要更改默认机会生成器使用的广告标记，请将包含自定义广告标记名称的矢量分配给 `adTags` 属性。

要接收有关HLS清单中的自定义标记的通知，请执行以下操作：

1. 通过将包含自定义标记的矢量分配给，全局设置自定义广告标记名称 `subscribeTags` 在 `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >您必须包含 `#` 使用HLS流时的前缀。

   例如：

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 要全局更改默认机会生成器使用的广告标记，请将包含自定义广告标记名称的矢量分配给 `adTags` 中的属性 `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 要使所有全局设置生效，请替换当前资源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 为流设置订阅的标记名称（如果需要）：
   1. 创建媒体播放器项目配置。

      >[!TIP]
      >
      >最简单的方法是创建默认媒体播放器项目配置。

   1. 将包含自定义标记的矢量分配给 `subscribeTags` 在 `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 要更改指定流中默认机会生成器使用的广告标记，请将包含自定义广告标记名称的矢量分配给 `adTags` 中的属性 `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 要使流的更改生效，请在加载媒体流时，使用媒体播放器项目配置。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
