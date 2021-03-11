---
description: 通过内容投放网络(CDN)交付的HLS流有时可以在清单和区段请求中使用身份验证令牌进行验证。 这些令牌可以作为URL参数或Cookie头提供。
title: 标记的区段流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 标记的段流{#tokenized-segment-streams}

通过内容投放网络(CDN)交付的HLS流有时可以在清单和区段请求中使用身份验证令牌进行验证。 这些令牌可以作为URL参数或Cookie头提供。

在主控清单(m3u8)响应上作为cookie提供的令牌不会与区段(ts)请求共享，即使区段请求是针对同一域的。 要在区段请求中启用这些Cookie的共享，请在提供给播放器项的`PTMetadata`实例上设置以下属性： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在流开始播放之前，对主控清单(m3u8)发出附加请求。

>[!IMPORTANT]
>
>仅运行iOS 8或更高版本的设备支持此Cookie共享功能。

