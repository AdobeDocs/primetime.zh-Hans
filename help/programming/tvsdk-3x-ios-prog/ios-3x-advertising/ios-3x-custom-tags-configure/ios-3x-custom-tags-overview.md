---
title: 自定义VOD资源示例
description: 自定义VOD资源示例
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 自定义VOD资源示例 {#example-of-a-customized-vod-asset}

以下是自定义VOD资源的示例：

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

您的应用程序可以设置以下方案：

* 通知时间 `#EXT-X-ASSET` 标记或您订阅的任何其他自定义标记名称集都存在于文件中。
* 插入广告条件 `#EXT-X-AD` 标记或任何其他自定义标记名称。
