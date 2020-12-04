---
seo-title: 自定义VOD资产的示例
title: 自定义VOD资产的示例
uuid: 25927d5f-ac16-45f4-bf0d-92f1ab394c05
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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

* 当文件中存在`#EXT-X-ASSET`标记或您订阅的任何其他自定义标记名称集时，将显示通知。
* 在流中找到`#EXT-X-AD`标记或任何其他自定义标记名称时插入广告。

