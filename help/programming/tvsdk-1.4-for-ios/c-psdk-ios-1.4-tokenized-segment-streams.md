---
description: 通过内容交付网络(CDN)交付的HLS流有时可在清单和段请求上使用身份验证令牌进行验证。 这些令牌可以作为URL参数或cookie头提供。
seo-description: 通过内容交付网络(CDN)交付的HLS流有时可在清单和段请求上使用身份验证令牌进行验证。 这些令牌可以作为URL参数或cookie头提供。
seo-title: 标记化的段流
title: 标记化的段流
uuid: b17bb5bc-2029-4113-ac44-b1d30aa08ca6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 标记化的段流{#tokenized-segment-streams}

通过内容交付网络(CDN)交付的HLS流有时可在清单和段请求上使用身份验证令牌进行验证。 这些令牌可以作为URL参数或cookie头提供。

在主清单(m3u8)响应上作为cookie提供的令牌不会与区段(ts)请求共享，即使区段请求是针对同一域的。 要在区段请求中启用这些cookie的共享，请对提供给播放器项的实 `PTMetadata` 例设置以下属性：

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在流开始播放之前，对主清单(m3u8)发出附加请求。

>[!IMPORTANT]
>
>仅运行iOS 8或更高版本的设备支持此Cookie共享功能。

