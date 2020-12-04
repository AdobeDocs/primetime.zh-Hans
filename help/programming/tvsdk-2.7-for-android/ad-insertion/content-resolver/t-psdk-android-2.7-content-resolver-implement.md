---
description: 您可以根据默认解析器实现您自己的内容解析器。
seo-description: 您可以根据默认解析器实现您自己的内容解析器。
seo-title: 实现自定义内容解析程序
title: 实现自定义内容解析程序
uuid: bc0eda17-9b5d-4733-8e93-790758e68df5
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---


# 实现自定义内容解析器{#implement-a-custom-content-resolver}

您可以根据默认解析器实现您自己的内容解析器。

当TVSDK生成新的机会时，它会重述已注册的内容解析器，寻找能够解决该机会的内容解析器。 选择返回`true`的第一个以解决该机会。 如果没有内容解析程序功能，则跳过该机会。 由于内容解析过程通常是异步的，因此内容解析程序负责在该过程完成时通知TVSDK。

1. 通过扩展`ContentFactory`接口并覆盖`retrieveResolvers`，实现您自己的自定义`ContentFactory`。

   例如：

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. 将`ContentFactory`注册到`MediaPlayer`。

   例如：

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. 将`AdvertisingMetadata`对象传递给TVSDK，如下所示：
   1. 创建`AdvertisingMetadata`对象。
   1. 将`AdvertisingMetadata`对象保存到`MediaPlayerItemConfig`。

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. 创建扩展`ContentResolver`类的自定义广告解析程序类。
   1. 在自定义广告解析程序中，覆盖`doConfigure`、`doCanResolve`、`doResolve`、`doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      您从`doConfigure`中传递的项获得`advertisingMetadata`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. 对于每个职位安排机会，创建一个`List<TimelineOperation>`。

      此示例`TimelineOperation`提供`AdBreakPlacement`的结构：

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. 解析广告后，调用以下功能之一：

      * 如果广告解析成功，请调用`ContentResolverClient`上的`process(List<TimelineOperation> proposals)`和`notifyCompleted(Opportunity opportunity)`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * 如果广告解析失败，请调用`ContentResolverClient`上的`notifyResolveError`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         例如：

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

此示例自定义广告解析程序解决了一个机会，并提供了一个简单的广告：

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

