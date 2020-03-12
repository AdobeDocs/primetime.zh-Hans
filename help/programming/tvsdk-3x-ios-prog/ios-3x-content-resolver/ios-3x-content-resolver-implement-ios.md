---
description: 您可以根据默认分辨率实现分辨率。
seo-description: 您可以根据默认分辨率实现分辨率。
seo-title: 实施自定义机会／内容解析程序
title: 实施自定义机会／内容解析程序
uuid: 0023f516-12f3-4548-93de-b0934789053b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 实施自定义机会／内容解析程序 {#implement-a-custom-opportunity-content-resolver}

您可以根据默认分辨率实现分辨率。

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. 通过扩展抽象类开发自定义广告解 `PTContentResolver` 析程序。

   `PTContentResolver` 是必须由内容解析器类实现的接口。 同名的抽象类也可用，并自动处理配置（获取委托）。

   >[!TIP]
   >
   >`PTContentResolver` 在课堂上暴露 `PTDefaultMediaPlayerClientFactory` 出来。 客户端可以通过扩展抽象类来注册新的内 `PTContentResolver` 容解析程序。 默认情况下，除非特别删除，否 `PTDefaultAdContentResolver` 则会在中注册 `PTDefaultMediaPlayerClientFactory`。

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. 如果 `shouldResolveOpportunity` 它应 `YES` 处理接收的内容，则执行并返回 `PTPlacementOpportunity`。
1. 实 `resolvePlacementOpportunity`施，开始加载替代内容或广告。
1. 加载广告后，准备一 `PTTimeline` 个包含要插入的内容相关信息的广告。

       以下是一些有关时间轴的有用信息：
   
   * 可以有多 `PTAdBreak`种预卷、中卷和后卷类型。

      * A具 `PTAdBreak` 有以下各项：

         * 具 `CMTimeRange` 有中断的开始时间和持续时间。

            这被设置为的范围属性 `PTAdBreak`。

         * `NSArray` `PTAd`s.

            此属性设置为的ads属性 `PTAdBreak`。
   * A代 `PTAd` 表广告，且每个广告 `PTAd` 都具有：

      * 设置 `PTAdHLSAsset` 为广告的主要资产属性。
      * 可能有多个 `PTAdAsset` 实例作为可点击广告或横幅广告。
   例如：

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. 拨 `didFinishResolvingPlacementOpportunity`叫，提供 `PTTimeline`。
1. 通过调用将自定义内容／广告解析程序注册到默认媒体播放器工厂 `registerContentResolver`。

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. 如果您实施了自定义业务机会解析程序，请将其注册到默认的媒体播放器工厂。

   >[!TIP]
   >
   >您不必注册自定义机会解析程序即可注册自定义内容／广告解析程序。

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

当播放器加载内容并确定其为VOD或LIVE类型时，将发生以下情况之一：

* 如果内容是VOD，则使用自定义内容解析程序获取整个视频的广告时间轴。
* 如果内容为LIVE，则每次在内容中检测到放置机会（提示点）时都会调用自定义内容解析程序。