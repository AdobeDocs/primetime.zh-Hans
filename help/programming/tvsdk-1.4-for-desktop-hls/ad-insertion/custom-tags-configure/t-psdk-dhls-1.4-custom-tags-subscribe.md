---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
title: 订阅自定义标记
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。

在播放开始之前，您必须订阅这些标记。
要订阅标记，请为`subscribedTags`属性指定包含自定义标记名称的矢量。 如果您还需要更改默认业务机会生成器使用的广告标签，请为`adTags`属性指定包含自定义广告标签名称的矢量。

要通知有关HLS清单中的自定义标记：

1. 通过将包含自定义标记的矢量分配给`MediaPlayerItemConfig`中的`subscribeTags`，全局设置自定义广告标记名称。

   >[!IMPORTANT]
   >
   >处理HLS流时必须包含`#`前缀。

   例如：

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 要全局更改默认业务机会生成器使用的广告标签，请将包含自定义广告标签名称的矢量分配给`PSDKConfig`中的`adTags`属性。

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 要使所有全局设置生效，请替换当前资源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 如果需要，要设置流的订阅标记名称：
   1. 创建媒体播放器项配置。

      >[!TIP]
      >
      >最简单的方法是创建默认媒体播放器项配置。

   1. 将包含自定义标记的矢量指定到`MediaPlayerItemConfig`中的`subscribeTags`。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 要更改指定流中默认机会生成器使用的广告标签，请将包含自定义广告标签名称的矢量分配给`mediaPlayerItemConfig`中的`adTags`属性

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 要使流的更改生效，请在加载媒体流时使用媒体播放器项配置。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

