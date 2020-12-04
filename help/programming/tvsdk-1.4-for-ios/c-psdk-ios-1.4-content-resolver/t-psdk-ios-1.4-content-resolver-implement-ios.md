---
description: 您可以根据默认的解析器实现解析器。
seo-description: 您可以根据默认的解析器实现解析器。
seo-title: 实施自定义机会／内容解析程序
title: 实施自定义机会／内容解析程序
uuid: bfc14318-ca4b-46cc-8128-e3743af06d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# 实现自定义机会／内容解析器{#implement-a-custom-opportunity-content-resolver}

您可以根据默认的解析器实现解析器。

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. 通过扩展`PTContentResolver`抽象类开发自定义广告解析程序。

   `PTContentResolver` 是必须由内容解析器类实现的接口。同名的抽象类也可用，并自动处理配置（获取委托）。

   >[!TIP]
   >
   >`PTContentResolver` 都暴露在课 `PTDefaultMediaPlayerClientFactory` 堂里。客户端可以通过扩展`PTContentResolver`抽象类注册新的内容解析程序。 默认情况下，除非特别删除，`PTDefaultAdContentResolver`将在`PTDefaultMediaPlayerClientFactory`中注册。

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

1. 如果应处理接收的`PTPlacementOpportunity`，则执行`shouldResolveOpportunity`并返回`YES`。
1. 实施`resolvePlacementOpportunity`，该&lt;a0/>开始加载替代内容或广告。
1. 加载广告后，准备一个`PTTimeline`，其中包含要插入的内容的相关信息。

       以下是一些有关时间轴的有用信息：
   
   * 可有多种`PTAdBreak`s的前滚、中滚和后滚类型。

      * `PTAdBreak`具有以下特性：

         * 具有中断开始时间和持续时间的`CMTimeRange`。

            它被设置为`PTAdBreak`的范围属性。

         * `NSArray`  `PTAd`s

            它设置为`PTAdBreak`的ads属性。
   * A `PTAd`表示广告，每个`PTAd`具有以下各项：

      * `PTAdHLSAsset`设置为广告的主资产属性。
      * 可能有多个`PTAdAsset`实例作为可点击广告或横幅广告。

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

1. 调用`didFinishResolvingPlacementOpportunity`，它提供`PTTimeline`。
1. 通过调用`registerContentResolver`将自定义内容／广告解析程序注册到默认媒体播放器工厂。

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. 如果您实现了自定义机会解析器，请将其注册到默认媒体播放器工厂。

   >[!TIP]
   >
   >您无需注册自定义机会解析程序即可注册自定义内容／广告解析程序。

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

当播放器加载内容并确定其为VOD或LIVE类型时，将发生以下情况之一：>
* 如果内容是VOD，则使用自定义内容解析程序获取整个视频的广告时间轴。
* 如果内容是LIVE，则每次在内容中检测到放置机会（提示点）时，都会调用自定义内容解析器。
