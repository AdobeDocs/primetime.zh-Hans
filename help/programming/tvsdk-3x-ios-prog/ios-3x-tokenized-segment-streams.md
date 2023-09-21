---
description: 通过内容交付网络(CDN)交付的HLS流有时可以使用清单上的身份验证令牌和区段请求进行验证。 这些令牌可以作为URL参数或Cookie标头提供。
title: 标记化的区段流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 标记化的区段流 {#tokenized-segment-streams}

通过内容交付网络(CDN)交付的HLS流有时可以使用清单上的身份验证令牌和区段请求进行验证。 这些令牌可以作为URL参数或Cookie标头提供。

在主清单(m3u8)响应中作为Cookie提供的令牌不会与区段(ts)请求共享，即使区段请求针对同一域也是如此。 要在区段请求中启用这些Cookie的共享，请在 `PTMetadata` 提供给播放器项目的实例： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在流开始播放之前，向主清单(m3u8)发出附加请求。

>[!IMPORTANT]
>
>只有运行iOS 8或更高版本的设备才支持此Cookie共享功能。
