---
description: 通过内容投放网络(CDN)交付的HLS流有时会在清单和段请求上使用身份验证令牌进行验证。 这些令牌可以作为URL参数或cookie头提供。
seo-description: 通过内容投放网络(CDN)交付的HLS流有时会在清单和段请求上使用身份验证令牌进行验证。 这些令牌可以作为URL参数或cookie头提供。
seo-title: 标记化段流
title: 标记化段流
uuid: 62e3b858-2605-4960-b504-9010674f80ad
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 标记化段流{#tokenized-segment-streams}

通过内容投放网络(CDN)交付的HLS流有时会在清单和段请求上使用身份验证令牌进行验证。 这些令牌可以作为URL参数或cookie头提供。

在主控清单(m3u8)响应上作为cookie提供的令牌不会与区段(ts)请求共享，即使区段请求是针对同一域的。 要在段请求中启用这些cookie的共享，请在提供给播放器项的`PTMetadata`实例上设置以下属性： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在流开始播放之前对主控清单(m3u8)发出附加请求。

>[!IMPORTANT]
>
>仅运行iOS 8或更高版本的设备支持此cookie共享功能。

