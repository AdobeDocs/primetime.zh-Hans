---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-title: 订阅自定义标记
title: 订阅自定义标记
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。

在播放开始之前，您必须订阅标记。
要订阅标记，请为`subscribedTags`属性指定包含自定义标记名称的矢量。 如果还需要更改默认机会生成器使用的广告标记，请为`adTags`属性指定包含自定义广告标记名称的矢量。

要通知有关HLS清单中的自定义标记：

1. 通过将包含自定义标记的矢量指定到`MediaPlayerItemConfig`中的`subscribeTags`，全局设置自定义广告标记名称。

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

1. 要全局更改默认业务机会生成器使用的广告标记，请将包含自定义广告标记名称的矢量分配给`PSDKConfig`中的`adTags`属性。

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 要使所有全局设置生效，请替换当前资源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 要为流设置订阅标记名称（如果需要）:
   1. 创建媒体播放器项配置。

      >[!TIP]
      >
      >最简单的方法是创建默认的媒体播放器项配置。

   1. 为`MediaPlayerItemConfig`中的`subscribeTags`指定包含自定义标记的矢量。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 要更改指定流中默认机会生成器使用的广告标签，请将包含自定义广告标签名称的矢量指定到`mediaPlayerItemConfig`中的`adTags`属性

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 要使流的更改生效，请在加载媒体流时，使用媒体播放器项配置。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

