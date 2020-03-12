---
seo-title: 自定义VOD资产的示例
title: 自定义VOD资产的示例
uuid: 21e83b47-d7e2-4a2d-8a0b-80dd09e253a8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 自定义VOD资产的示例 {#example-of-a-customized-vod-asset}

以下是自定义VOD资产的示例：

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

您的应用程序可以设置以下场景：

* 文件中存 `#EXT-X-ASSET` 在标记或您订阅的任何其他自定义标记名称集时的通知。
* 在流中找到标 `#EXT-X-AD` 记或任何其他自定义标记名称时插入广告。

