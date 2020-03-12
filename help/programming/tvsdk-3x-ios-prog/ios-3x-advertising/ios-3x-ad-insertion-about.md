---
description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需的请求，接收有关指定内容的广告的信息，并将广告分阶段放入内容中。
seo-description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需的请求，接收有关指定内容的广告的信息，并将广告分阶段放入内容中。
seo-title: 插入广告
title: 插入广告
uuid: 6e31cae5-7363-454f-82dd-e03c1e34cd3f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 插入广告 {#insert-ads}

广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需的请求，接收有关指定内容的广告的信息，并将广告分阶段放入内容中。

An包 *`ad break`* 含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告分段的成员插入主内容中。

>[!TIP]
>
>如果广告有错误，TVSDK将忽略该广告。

## 解析和插入VOD广告 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK支持多个用于VOD广告解析和插入的用例。

* 前置广告插入，其中广告插入内容的开头。
* 中间广告插入，其中至少一个广告被插入到内容的中间。
* 广告插入后，其中在内容的末尾附加至少一个广告。

TVSDK解析广告，将广告插入广告服务器定义的位置，并在播放开始前计算虚拟时间轴。 播放开始后，不会发生任何更改，如插入广告或删除插入广告。

## 解析和插入实时和线性广告 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK支持多个用于实时和线性广告解析和插入的用例。

* 预卷广告插入，其中在内容的开头插入至少一个广告。
* 中间广告插入，其中至少一个广告被插入到内容的中间。

TVSDK解析广告，并在实时或线性流中遇到提示点时插入广告。 默认情况下，TVSDK在解析和放置广告时支持以下提示作为有效的广告标记：

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

这些标记需要元数据字段(以 `DURATION` 秒为单位)和提示的唯一ID。 例如：

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

有关其他提示的详细信息，请参 [阅订阅自定义标记](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md)。

## 跟踪客户端广告 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK可自动跟踪VOD和实时／线性流的广告。

通知用于通知您的应用程序广告进度，包括广告开始时间和结束时间的相关信息。

## 实施早期广告分时段退货 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。

以下是一些早期广告分时段返回的示例：

* 某些体育赛事中广告中断的持续时间。

   尽管提供了默认持续时间，但如果游戏在中断结束前继续，则必须退出广告中断。
* 实时流中广告中断期间的紧急信号。

通过清单中称为剪接或提示标记的自定义标记识别早期退出广告中断的能力。 TVSDK允许应用程序订阅这些拼接标记，以提供拼接机会。

* 要将标签 `#EXT-X-CUE-IN` 用作拼接机会并实现早期广告中断返回，请执行以下操作：

   1. 订阅标记。

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. 添加提示机会解析器。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* 要共享同一标签进行剪接和剪接：

1. 如果应用程序共享指示提示输出／剪接输出和提示输入／剪接输入的同一提示，则扩展并 `PTDefaultAdOpportunityResolver` 实现该方 `preparePlacementOpportunity` 法。

   [!TIP]

   以下代码假定应用程序具有该方法的实 `isCueInOpportunity` 现。

```
   - (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
   { 
         if ([self isCueInOpportunity:timedMetadata]) 
         { 
               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
           } 
           else 
           { 
               return [super preparePlacementOpportunity:timedMetadata]; 
         } 
   }
```

1. 在实例上注册扩展业务机会解 `PTDefaultMediaPlayerClientFactory` 析程序。

```
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
