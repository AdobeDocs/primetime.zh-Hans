---
title: 自定义VOD资产的示例
description: 自定义VOD资产的示例
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# 自定义VOD资产的示例{#example-of-a-customized-vod-asset}

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

* 当`#EXT-X-ASSET`标记或您订阅的任何其他自定义标记名称集存在于文件中时的通知。
* 在流中找到`#EXT-X-AD`标记或任何其他自定义标记名称时插入广告。

