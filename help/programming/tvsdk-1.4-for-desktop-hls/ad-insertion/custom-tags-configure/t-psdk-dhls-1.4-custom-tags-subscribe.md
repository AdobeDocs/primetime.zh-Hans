---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-title: 订阅自定义标记
title: 订阅自定义标记
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。

在播放开始之前，您必须订阅标记。
要订阅标记，请为属性指定包含自定义标记名称的矢 `subscribedTags` 量。 如果您还需要更改默认业务机会生成器使用的广告标记，请为属性分配一个包含自定义广告标记名称的矢 `adTags` 量。

要获得有关HLS清单中自定义标记的通知，请执行以下操作：

1. 通过将包含自定义标记的矢量指定到中来全局设置自定义广告标 `subscribeTags` 记名称 `MediaPlayerItemConfig`。

   >[!IMPORTANT]
   >
   >处理HLS流时 `#` 必须包含前缀。

   例如：

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 要全局更改默认业务机会生成器使用的广告标记，请为中的属性指定包含自定义广告标记名称的 `adTags` 矢量 `PSDKConfig`。

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 要使所有全局设置生效，请替换当前资源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 如果需要，为流设置订阅的标记名称：
   1. 创建媒体播放器项配置。

      >[!TIP]
      >
      >最简单的方法是创建默认的媒体播放器项目配置。

   1. 指定包含中的自定义标记的 `subscribeTags` 矢量 `MediaPlayerItemConfig`。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 要更改指定流中默认业务机会生成器使用的广告标签，请将包含自定义广告标签名称的矢量分配到 `adTags``mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 要使流的更改生效，请在加载媒体流时使用媒体播放器项配置。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

