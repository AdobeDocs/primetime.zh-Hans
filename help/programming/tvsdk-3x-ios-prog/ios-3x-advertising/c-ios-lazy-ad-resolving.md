---
description: 广告解析和广告加载可能会导致等待播放开始的用户出现不可接受的延迟。 延迟广告加载解决功能可减少此启动延迟。 现在可以在广告时间位置之前的指定间隔解析广告。 这是通过使用双玩家方法实现的。
title: 及时广告解析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 及时广告解析 {#just-in-time-ad-resolving}

广告解析和广告加载可能会导致等待播放开始的用户出现不可接受的延迟。 延迟广告加载解决功能可减少此启动延迟。 现在可以在广告时间位置之前的指定间隔解析广告。 这是通过使用双玩家方法实现的。

**基本广告解析和加载流程：**

1. TVSDK下载清单（播放列表）和 *解析* 所有广告。
1. TVSDK *加载* 所有广告并将广告区段拼合到清单中。
1. TVSDK将播放器移到“已准备”状态，并开始播放内容。

播放器使用清单中的URL获取广告内容（创意），确保广告内容采用TVSDK可以播放的格式，并且TVSDK将广告放在时间轴上。 这种解析和加载广告的基本流程可能会导致等待播放其内容的用户出现不可接受的长延迟，尤其是当清单包含多个广告URL时。

**延迟广告解决：**

1. TVSDK将下载播放列表。
1. TVSDK *解析并加载* 任何前置广告，都会将播放器移到“已准备”状态，并开始播放内容。
1. TVSDK *解析* 每个广告在其位置之前根据中定义的值中断 `PTAdMetadata::delayAdLoadingTolerance`.

例如，默认情况下 `delayAdLoadingTolerance` 设置为5秒。 如果将AdBreak设置为在3:00播放，则将在2进行解析:55:00。 如果您认为广告分辨率需要超过5秒的时间，则可能需要增加此值。

>[!IMPORTANT]
>
>**考虑延迟广告解决的因素：**
>* 延迟广告解析仅支持具有模式SERVER_MAP和信令模式的VOD流。
>* 默认情况下不启用延迟广告解析。 您必须设置 `PTAdMetadata::delayAdLoading` =“是”以启用它。
>* 延迟广告解析与立即启用功能不兼容。 有关Instant On的详细信息，请参见 [即时打开](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* 延迟广告解析不支持画中画模式。 如果启用延迟广告解析，请禁用任何画中画模式。
>* 延迟广告分辨率不会影响前置广告。
>
**启用延迟广告解析**

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。

您可以通过设置来启用延迟广告解析 `PTAdMetadata::delayAdLoading`=设置广告元数据时为“是”。

**与延迟广告解析相关的API：**

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
