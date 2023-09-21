---
description: 您可以基于默认解析器实施自己的内容解析器。
title: 实施自定义内容解析程序
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 实施自定义内容解析程序 {#implement-a-custom-content-resolver}

您可以基于默认解析器实施自己的内容解析器。

当TVSDK生成新的机会时，它通过注册的内容解析器不断寻找能够解析该机会的机会。 第一个返回 `true` 已选中以解决商机。 如果没有任何内容解析程序能够解析内容，则会跳过该机会。 由于内容解析过程通常是异步的，因此内容解析程序负责在过程完成后通知TVSDK。

1. 实施您自己的自定义 `ContentFactory`，通过扩展 `ContentFactory` 界面和覆盖 `retrieveResolvers`.

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

1. 注册 `ContentFactory` 到 `MediaPlayer`.

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

1. 传递 `AdvertisingMetadata` 对象，如下所示：
   1. 创建 `AdvertisingMetadata` 对象。
   1. 保存 `AdvertisingMetadata` 对象对象 `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. 创建一个自定义广告解析程序类，以扩展 `ContentResolver` 类。
   1. 在自定义广告解析程序中，覆盖 `doConfigure`， `doCanResolve`， `doResolve`， `doCleanup`：

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      你得到你的 `advertisingMetadata` 来自传入的项目 `doConfigure`：

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. 对于每个投放机会，创建 `List<TimelineOperation>`.

      此示例 `TimelineOperation` 为以下对象提供结构 `AdBreakPlacement`：

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. 解决广告后，调用以下函数之一：

      * 如果广告解析成功，请调用 `process(List<TimelineOperation> proposals)` 和 `notifyCompleted(Opportunity opportunity)` 在 `ContentResolverClient`

        ```java
        _client.process(timelineOperations); 
        _client.notifyCompleted(opportunity); 
        ```

      * 如果广告解析失败，请调用 `notifyResolveError` 在 `ContentResolverClient`

        ```java
        _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
        ```

        例如：

        ```java
        _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
        ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

此示例自定义广告解析程序可解析一个机会并提供一个简单的广告：

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
