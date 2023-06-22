---
description: 广告插入可解析以下内容的广告：视频点播(VOD) 、实时流以及带有广告跟踪和广告播放的线性流。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。
title: 插入广告
exl-id: 4e5a4fe2-6887-48d0-b335-f3e99559dca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 插入广告{#insert-ads}

广告插入可解析以下内容的广告：视频点播(VOD) 、实时流以及带有广告跟踪和广告播放的线性流。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。

An *`ad break`* 包含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告时间的成员，插入主内容中。

>[!TIP]
>
>如果广告有错误，TVSDK会忽略该广告。

## 解析和插入VOD广告 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK支持多个VOD广告解析和插入用例。

* 前置广告插入，将广告插入在内容的开头。
* 中置广告插入，其中至少一个广告插入内容中间。
* 后置广告插入，其中至少一个广告被附加在内容的末尾。

TVSDK解析广告，将广告插入广告服务器定义的位置，并在播放开始之前计算虚拟时间轴。 播放开始后，不会发生任何更改，例如插入的广告或移除插入的广告。

## 解析并插入实时和线性广告 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK支持实时和线性广告解析和插入的多个用例。

* 前置广告插入，其中在内容的开头插入至少一个广告。
* 中置广告插入，其中至少一个广告插入内容中间。

当在实时流或线性流中遇到提示点时，TVSDK会解析广告并插入广告。 默认情况下，TVSDK在解析和放置广告时支持以下提示作为有效的广告标记：

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

这些标记需要元数据字段的 `DURATION` 以秒为单位，并且提示的唯一ID为。 例如：

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

有关其他提示的更多信息，请参阅 [订阅自定义标记](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## 跟踪客户端广告 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK会自动跟踪VOD和实时/线性流播放的广告。

通知用于通知应用程序广告的进度，包括有关广告何时开始和何时结束的信息。

## 实施提前返回广告时间 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

对于实时流广告插入，您可能需要先退出广告时间，然后再播放广告时间中的所有广告直至结束。

以下是提前返回广告时间的一些示例：

* 某些体育赛事中的广告插播持续时间。

   虽然提供了默认持续时间，但如果游戏在休息时间结束前恢复，则必须退出广告时间。
* 在实时流中的广告时间期间的紧急信号。

通过清单中的自定义标记（称为插入或提示加入标记）来识别提前退出广告时间的能力。 TVSDK允许应用程序订阅这些插入标记以提供插入机会。

* 要使用 `#EXT-X-CUE-IN` 标记为插入机会并实现广告时间的早期回报：

   1. 订阅标记。

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. 添加提示机会解析程序。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* 要共享相同的标记以进行剪切和剪切，请执行以下操作：

   1. 如果应用程序共享相同的提示来指示提示输出/接合输出和提示输入/接入，则扩展 `PTDefaultAdOpportunityResolver` 并实施 `preparePlacementOpportunity` 方法。

      >[!TIP]
      >
      >以下代码假定应用程序具有 `isCueInOpportunity` 方法。
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

   1. 在注册扩展机会解析程序 `PTDefaultMediaPlayerClientFactory` 实例。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```
