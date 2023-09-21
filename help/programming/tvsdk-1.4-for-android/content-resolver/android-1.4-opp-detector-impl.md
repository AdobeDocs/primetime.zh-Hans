---
description: 通过实施PlacementOpportunityDetector接口，您可以实施自己的机会检测器。
title: 实施自定义机会检测器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 实施自定义机会检测器 {#implement-a-custom-opportunity-detector}

通过实施PlacementOpportunityDetector接口，您可以实施自己的机会检测器。

1. 创建自定义 `AdvertisingFactory` 实例和覆盖 `createOpportunityDetector`. 例如：

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

1. 将广告客户端工厂注册到 `MediaPlayer`. 例如：

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 创建一个自定义机会检测器类，以扩展 `PlacementOpportunityDetector` 类。
   1. 在自定义机会检测器中，覆盖此函数：

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      此 `timedMetadataList` 包含可用列表 `TimedMetadata`，进行排序。 元数据包含定位参数和要发送到广告提供商的自定义参数。

   1. 对于每个 `TimedMetadata`，创建 `List<PlacementOpportunity>`. 列表可以为空，但不能为null。 `PlacementOpportunity` 应具有以下属性：

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 在为所有检测到的定时元数据对象创建投放机会后，只需返回 `PlacementOpportunity` 列表。

这是一个自定义投放位置机会检测器示例：

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
