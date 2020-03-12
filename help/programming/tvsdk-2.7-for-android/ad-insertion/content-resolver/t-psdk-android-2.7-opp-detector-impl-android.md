---
description: 您可以通过实施OpportunityGenerator类来实施您自己的机会生成器。
seo-description: 您可以通过实施OpportunityGenerator类来实施您自己的机会生成器。
seo-title: 实施自定义机会生成器
title: 实施自定义机会生成器
uuid: 93d8253f-10f9-4950-a273-28975cb69caa
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 实施自定义机会生成器 {#implement-a-custom-opportunity-generator}

您可以通过实施OpportunityGenerator类来实施您自己的机会生成器。

1. 通过实现接 `ContentFactory` 口和覆盖来实 `ContentFactory` 现自定义 `retrieveGenerators`。

   例如：

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
           List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
           generators.add(MyOpportunityGenerator(item)); 
           return generators; 
       } 
       ... 
   }
   ```

1. 将其注 `ContentFactory` 册到 `MediaPlayer`。

   例如：

   ```java
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. 创建实现该类的自定义业务机会生成 `OpportunityGenerator` 器类。

   ```java
   public class CustomOpportunityGenerator implements OpportunityGenerator  
   {...}
   ```

   1. 在自定义业务机会生成器中， `doConfigure`覆盖 `doUpdate` 和 `doCleanup`:

      ```java
      @Override 
       public void configure(MediaPlayerItem item, Context context,  
       OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
      
      protected void update(long playhead, TimeRange playbackRange){ 
      } 
      
      protected void cleanup(){ 
      }
      ```

      要获取定时元数据，请执行以下操作：

      ```java
      List<TimedMetadata> tList = getItem().getTimedMetadata(); 
      ```

   1. 对于每个 `TimedMetadata` 或一组， `TimedMetadata`请创建具有以下属性的业务机会：

      ```java
      Opportunity( 
        String id,                      // Can be id from timedMetadata  
        Placement placementInformation, // Placement object containing Type, time, duration 
        Metadata metadataSettings,      // Ad metadata with targeting params sent to the ad provider 
        Metadata customParams           // Metadata for customizing resolving and/or tracking process. 
      ); 
      ```

   1. 对于创建的每个机会，请 `resolve` 拔打电话 `OpportunityGeneratorClient:getClient().resolve(opportunity);`。

<!--<a id="example_7A46377EBE79458E87423EB95D0568D4"></a>-->

这是一个示例自定义放置机会检测器：

```java
public class MyOpportunityGenerator implements OpportunityGenerator {

     @Override 
      public void configure(MediaPlayerItem item, Context context,  
      OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
 
        MediaPlayerItem item = getItem(); 
        MediaPlayerItemConfig itemConfig = item.getConfig(); 
 
        if (itemConfig == null || itemConfig.getAdvertisingMetadata() == null) { 
            // no ad metadata, no ads 
            return; 
        } 
 
        AdvertisingMetadata metadata = item.getConfig().getAdvertisingMetadata();

        AdSignalingMode mode = itemConfig.getAdSignalingMode(); 
 
        if (mode == AdSignalingMode.CUSTOM_RANGES) 
        { 
            // don't override custom ad ranges 
            return; 
        } 
 
        Placement.Type pType = (mode == AdSignalingMode.MANIFEST_CUES) ?  
                  Placement.Type.PRE_ROLL : Placement.Type.SERVER_MAP; 
        Placement.Mode pMode = Placement.Mode.DEFAULT; 
        Placement placement = new Placement(pType, playhead,  
                  Placement.UNKNOWN_DURATION, pMode); 
 
        Opportunity opportunity = new Opportunity("initialOpportunity", placement,  
                  metadata, null); 
 
        OpportunityGeneratorClient client = getClient(); 
        client.resolve(opportunity); 
    } 
 
    @Override 
    protected void update(long playhead, TimeRange playbackRange) { 
 
 ... 
 timedMetadataList = getItem().getTimedMetadata(); 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
         if (isOpportunity(timedMetadata)) {   // check if given timedMetadata should  
                                               // be considered as an opportunity 
  // create a PlacementOpportunity object and add it to the opportunities list 
                Opportunity opportunity = new Opportunity("id", placement, metadata, null); 
                client.resolve(opportunity) 
          } 
        } 
    } 
 
    @Override 
    protected void cleanup() {} 
}
```

