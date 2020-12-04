---
description: 广告解析和广告加载可能会给等待播放到开始的用户造成不可接受的延迟。 延迟广告加载解析功能可减少此启动延迟。 现在，广告可以在广告中断位置之前以指定的间隔解析。 这是通过使用双玩家方法实现的。
seo-description: 广告解析和广告加载可能会给等待播放到开始的用户造成不可接受的延迟。 延迟广告加载解析功能可减少此启动延迟。 现在，广告可以在广告中断位置之前以指定的间隔解析。 这是通过使用双玩家方法实现的。
seo-title: 及时广告解决
title: 及时广告解决
uuid: f7b20439-3604-4d69-bdfe-2e0ad26f495b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# 即时广告解决{#just-in-time-ad-resolving}

广告解析和广告加载可能会给等待播放到开始的用户造成不可接受的延迟。 延迟广告加载解析功能可减少此启动延迟。 现在，广告可以在广告中断位置之前以指定的间隔解析。 这是通过使用双玩家方法实现的。

**基本广告解析和加载流程：**

1. TVSDK下载清单（播放列表）,*resolves*&#x200B;所有广告。
1. TVSDK *加载*&#x200B;所有广告并将广告片段拼接到清单中。
1. TVSDK将播放器移入PREPARED状态，内容播放开始。

播放器使用清单中的URL获取广告内容（创意），确保广告内容采用TVSDK可播放的格式，而TVSDK将广告放在时间轴上。 解析和加载广告的这一基本过程可能会给等待播放其内容的用户带来无法接受的长时间延迟，尤其是当清单包含多个广告URL时。

**延迟广告解决：**

1. TVSDK下载播放列表。
1. TVSDK *解析并加载*&#x200B;任何预先滚动广告，将播放器移入PREPARED状态，内容播放开始。
1. TVSDK *根据`PTAdMetadata::delayAdLoadingTolerance`中定义的值解析*&#x200B;每个广告在其位置之前断开。

例如，默认情况下`delayAdLoadingTolerance`设置为5秒。 如果AdBreak设置为在3:00播放，则将在2:55:00解决该问题。 如果您认为广告分辨率将超过5秒，则可能希望增加此值。

>[!IMPORTANT]
>
>**懒惰广告解决时要考虑的因素：**
>* 延迟广告解析仅支持具有SERVER_MAP和信令模式的VOD流。
>* 默认情况下不启用延迟广告解析。 必须设置`PTAdMetadata::delayAdLoading` = YES才能启用它。
>* 延迟广告解析与“即时开启”功能不兼容。 有关“即时打开”的详细信息，请参阅[“即时打开”](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)。
>* 延迟广告解析不支持画中画模式。 如果启用延迟广告解析，请禁用任何画中画模式。
>* 延迟广告解决不会影响预放广告。

>


**启用延迟广告解析**

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。

在设置广告元数据时，可以通过设置`PTAdMetadata::delayAdLoading`= YES来启用延迟广告解析。

**与懒惰广告解析相关的API:**

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
