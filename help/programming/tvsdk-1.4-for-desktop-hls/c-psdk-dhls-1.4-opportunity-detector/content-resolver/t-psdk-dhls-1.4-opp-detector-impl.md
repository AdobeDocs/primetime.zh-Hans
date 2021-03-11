---
description: 您可以实施您自己的机会检测器。
title: 实施自定义机会检测器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 实现自定义机会检测器{#implement-a-custom-opportunity-detector}

您可以实施您自己的机会检测器。

* 如果您的机会生成器基于与当前媒体流关联的`TimedMetadata`对象，则它应扩展`SpliceOutOpportunityGenerator`或`TimedMetadataOpportunityGenerator`。

* 如果您的机会生成器基于外部服务（如CIS）提供的带外数据，则它应扩展`OpportunityGenerator`。

1. 创建自定义机会生成器。

       如果您的自定义业务机会生成器基于“TimedMetadata”对象，则扩展“TimedMetadataOpportunityGenerator”并覆盖以下方法：
   
   * `doConfigure`  — 在创建媒体播放器项目后调用此方法，并提供机会生成器以根据需要创建初始机会集
   * `doProcess`  — 每次检测到新内容时都会调 `TimedMetadata` 用此方法（例如，每次播放列表/清单刷新时，对实时/线性流调用此方法）

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

