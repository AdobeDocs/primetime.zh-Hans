---
description: 您可以通过实现接口PlacementOpportunityDetector来实现您自己的机会检测器。
title: 实施自定义机会检测器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# 实现自定义机会检测器{#implement-a-custom-opportunity-detector}

您可以通过实现接口PlacementOpportunityDetector来实现您自己的机会检测器。

1. 创建自定义`AdvertisingFactory`实例并覆盖`createOpportunityDetector`。 例如：

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. 向`MediaPlayer`注册广告客户端工厂。 例如：

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 创建扩展`PlacementOpportunityDetector`类的自定义机会检测器类。
   1. 在自定义机会检测器中，覆盖此函数：

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      `timedMetadataList`包含可用`TimedMetadata`的列表，该字段已排序。 元数据包含要发送到广告提供者的定位参数和自定义参数。

   1. 对于每个`TimedMetadata`，创建一个`List<PlacementOpportunity>`。 列表可以为空，但不能为null。 `PlacementOpportunity` 应具有以下属性：

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 为检测到的所有定时元数据对象创建放置机会后，只需返回`PlacementOpportunity`列表。

这是一个自定义放置机会检测器示例：

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```

