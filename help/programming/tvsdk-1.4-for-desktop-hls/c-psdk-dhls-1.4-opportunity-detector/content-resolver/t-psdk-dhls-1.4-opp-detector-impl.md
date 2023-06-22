---
description: 您可以实施自己的机会检测器。
title: 实施自定义机会检测器
exl-id: a3f6d6b3-4d5e-49bc-b8de-a1196305bbb4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 实施自定义机会检测器{#implement-a-custom-opportunity-detector}

您可以实施自己的机会检测器。

* 如果您的机会生成器基于 `TimedMetadata` 与当前媒体流关联的对象，则它应扩展 `SpliceOutOpportunityGenerator` 或 `TimedMetadataOpportunityGenerator`.

* 如果您的机会生成器基于外部服务（如CIS）提供的带外数据，则它应扩展 `OpportunityGenerator`.

1. 创建自定义机会生成器。

       如果您的自定义机会生成器基于“TimedMetadata”对象，请扩展“TimedMetadataOpportunityGenerator”并覆盖以下方法：
   
   * `doConfigure`  — 在创建媒体播放器项目后调用此方法，并提供机会生成器以根据需要创建初始机会集
   * `doProcess`  — 每次新建时都调用此方法 `TimedMetadata` 检测（例如，对于实时/线性流，每次播放列表/清单刷新时）

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

1. 创建使用自定义机会生成器的自定义内容工厂。

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
