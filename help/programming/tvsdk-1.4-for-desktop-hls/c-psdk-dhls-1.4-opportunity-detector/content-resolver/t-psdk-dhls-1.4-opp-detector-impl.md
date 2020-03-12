---
description: 您可以实施自己的机会检测器。
seo-description: 您可以实施自己的机会检测器。
seo-title: 实施自定义机会检测器
title: 实施自定义机会检测器
uuid: 18fb431b-4585-4293-92a7-b77ab7f9b7db
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 实施自定义机会检测器{#implement-a-custom-opportunity-detector}

您可以实施自己的机会检测器。

* 如果您的业务机会生成器基 `TimedMetadata` 于与当前媒体流关联的对象，则它应该扩展 `SpliceOutOpportunityGenerator` 或 `TimedMetadataOpportunityGenerator`。

* 如果您的机会生成器基于由外部服务（如CIS）提供的带外数据，那么它应该扩展 `OpportunityGenerator`。

1. 创建自定义机会生成器。

       如果您的自定义业务机会生成器基于“TimedMetadata”对象，则扩展“TimedMetadataOpportunityGenerator”并覆盖以下方法：
   
   * `doConfigure` -在创建媒体播放器项目后调用此方法，并根据需要提供机会生成器以创建初始机会集
   * `doProcess` -每次检测到新内容时都会调 `TimedMetadata` 用此方法（例如，每次播放列表／清单刷新时，对于实时／线性流）

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. 创建自定义内容工厂，它使用自定义机会生成器。

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. 为要播放的媒体流注册自定义内容工厂。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

