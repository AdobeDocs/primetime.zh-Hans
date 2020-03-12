---
description: 广告解析和广告加载可能导致等待播放的用户出现无法接受的延迟。 “延迟广告加载解决”功能可以减少此启动延迟。 广告现在可以在广告中断位置之前的指定间隔内解析。 这是通过使用双玩家方法实现的。
seo-description: 广告解析和广告加载可能导致等待播放的用户出现无法接受的延迟。 “延迟广告加载解决”功能可以减少此启动延迟。 广告现在可以在广告中断位置之前的指定间隔内解析。 这是通过使用双玩家方法实现的。
seo-title: 即时广告解决
title: 即时广告解决
uuid: f7b20439-3604-4d69-bdfe-2e0ad26f495b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 即时广告解决 {#just-in-time-ad-resolving}

广告解析和广告加载可能导致等待播放的用户出现无法接受的延迟。 “延迟广告加载解决”功能可以减少此启动延迟。 广告现在可以在广告中断位置之前的指定间隔内解析。 这是通过使用双玩家方法实现的。

**基本广告解析和加载流程：**

1. TVSDK下载清单（播放列表）并 *解析* 所有广告。
1. TVSDK加 *载所有广告* ，并将广告段编入清单。
1. TVSDK将播放器移入PREPARED状态，内容播放开始。

播放器使用清单中的URL获取广告内容（创意），确保广告内容采用TVSDK可播放的格式，而TVSDK将广告放在时间轴上。 解析和加载广告的这一基本过程可能导致用户等待播放其内容的长时间延迟，尤其是当清单包含多个广告URL时。

**延迟广告解决：**

1. TVSDK下载播放列表。
1. TVSDK解 *析并加载任何预先播放的广告* ，将播放器移入PREPARED状态，内容播放开始。
1. TVSDK *根据* （中定义的值）解析每个广告中断在其位置之前的位置 `PTAdMetadata::delayAdLoadingTolerance`。

例如，默认情 `delayAdLoadingTolerance` 况下设置为5秒。 如果AdBreak设置为在3:00播放，则会在2:55:00解决它。 如果您认为广告分辨率将超过5秒，则可能希望增加此值。

>[!IMPORTANT]
>
>**懒惰广告解决应考虑的因素：**
>* 仅支持SERVER_MAP和信令模式的VOD流支持延迟广告解析。
>* 默认情况下，“延迟广告解析”未启用。 必须设置 `PTAdMetadata::delayAdLoading` 为= YES才能启用它。
>* “延迟广告解析”与“即时打开”功能不兼容。 有关“即时开启”的详细信息，请参 [阅“即时开启”](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)。
>* 延迟广告解析不支持画中画模式。 如果您启用“延迟广告解析”，请禁用任何画中画模式。
>* 延迟广告解决不会影响预先投放广告。
>


**启用延迟广告解决**

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，延迟广告解析处于禁用状态）。

在设置广告元数据时，可以通 `PTAdMetadata::delayAdLoading`过设置= YES来启用延迟广告解析。

**与延迟广告解析相关的API:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
