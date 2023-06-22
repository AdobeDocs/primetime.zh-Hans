---
description: 源列表中的forceflash标记可强制URL的Flash回退。 对于此URL，您可以使用AdobeFlash Player播放内容。
title: 使用媒体源列表强制Flash回退
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 使用媒体源列表强制Flash回退{#forcing-the-flash-fallback-using-the-media-source-list}

源列表中的forceflash标记可强制URL的Flash回退。 对于此URL，您可以使用AdobeFlash Player播放内容。

在媒体源列表中(例如 `sources.js` 文件)，您可以设置 `forceflash` 到 `true`. 例如：

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```
