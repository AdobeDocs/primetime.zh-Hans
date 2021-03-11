---
description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需请求，接收指定内容的广告信息，并分阶段将广告放入内容中。
title: 插入广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# 插入广告{#insert-ads}

广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需请求，接收指定内容的广告信息，并分阶段将广告放入内容中。

*`ad break`*&#x200B;包含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告分段的成员插入主内容中。

>[!TIP]
>
>如果广告有错误，TVSDK将忽略该广告。

## 解析和插入VOD广告{#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK支持VOD广告解析和插入的几个用例。

* 前置广告插入，其中广告插入内容的开头。
* 中间广告插入，其中至少一个广告插入到内容的中间。
* 后置广告插入，其中在内容末尾附加至少一个广告。

TVSDK解析广告，将广告插入广告服务器定义的位置，并在播放开始之前计算虚拟时间线。 播放开始后，不会发生任何更改，如插入的广告或删除的插入广告。

## 解析并插入实时和线性广告{#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK支持实时和线性广告解析和插入的几个用例。

* 预卷广告插入，其中在内容的开头插入至少一个广告。
* 中间广告插入，其中至少一个广告插入到内容的中间。

TVSDK解析广告，并在实时或线性流中遇到提示点时插入广告。 默认情况下，TVSDK在解析和放置广告时支持以下提示作为有效的广告标记：

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

这些标记要求元数据字段的`DURATION`（以秒为单位）和提示的唯一ID。 例如：

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

有关其他提示的详细信息，请参阅[订阅自定义标签](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md)。

## 跟踪客户端和{#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK自动跟踪VOD和实时/线性流的广告。

通知用于通知您的应用程序广告的进度，包括广告开始和结束时的相关信息。

## 实施早期广告中断返回{#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

对于实时流广告插入，您可能需要先退出广告中断，然后再播放中断中的所有广告以完成。

以下是一些早期广告分时段返回的示例：

* 某些体育事件中广告中断的持续时间。

   尽管提供了默认持续时间，但如果游戏在中断结束前继续，则必须退出广告中断。
* 实时流中广告中断期间的紧急信号。

通过清单中称为剪接或提示标记的定制标记来识别提前退出广告中断的能力。 TVSDK允许应用程序订阅这些剪接入标签以提供剪接入机会。

* 要将`#EXT-X-CUE-IN`标签用作插入机会并实现早期广告中断返回：

   1. 订阅标签。

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

* 要共享同一标签以进行拼接和拼接：

   1. 如果应用程序共享指示提示/剪接和提示/剪接的相同提示，请扩展`PTDefaultAdOpportunityResolver`并实现`preparePlacementOpportunity`方法。

      >[!TIP]
      >
      >以下代码假定应用程序具有`isCueInOpportunity`方法的实现。
      >
      >
      ```
      >- (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
      >{ 
      >       if ([self isCueInOpportunity:timedMetadata]) 
      >       { 
      >               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
      >       } 
      >       else 
      >       { 
      >               return [super preparePlacementOpportunity:timedMetadata]; 
      >       } 
      >}
      >```

   1. 在`PTDefaultMediaPlayerClientFactory`实例上注册扩展机会解析程序。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

