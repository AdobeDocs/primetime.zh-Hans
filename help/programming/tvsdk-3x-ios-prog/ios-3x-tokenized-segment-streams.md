---
description: 通过内容交付网络(CDN)交付的HLS流有时可以使用清单上的身份验证令牌和区段请求进行验证。 这些令牌可以作为URL参数或Cookie标头提供。
title: 标记化的区段流
exl-id: c7b441a7-63b6-4930-93a1-12ef6b72474e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 标记化的区段流 {#tokenized-segment-streams}

通过内容交付网络(CDN)交付的HLS流有时可以使用清单上的身份验证令牌和区段请求进行验证。 这些令牌可以作为URL参数或Cookie标头提供。

即使区段请求是针对同一域的，主控清单(m3u8)响应中作为Cookie提供的令牌也不会与区段(ts)请求共享。 要在区段请求中启用这些Cookie共享，请在 `PTMetadata` 提供给播放器项目的实例： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在开始播放流之前，会向主控清单(m3u8)发出附加请求。

>[!IMPORTANT]
>
>只有运行iOS 8或更高版本的设备才支持此Cookie共享功能。
