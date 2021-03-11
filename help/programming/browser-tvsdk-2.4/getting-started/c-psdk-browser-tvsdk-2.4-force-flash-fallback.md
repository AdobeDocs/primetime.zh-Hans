---
description: 源列表中的forceflash标志强制Flash回退URL。 对于此URL，可以使用AdobeFlash Player播放内容。
title: 使用媒体源Flash强制列表回退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# 使用媒体源Flash{#forcing-the-flash-fallback-using-the-media-source-list}强制列表回退

源列表中的forceflash标志强制Flash回退URL。 对于此URL，可以使用AdobeFlash Player播放内容。

在媒体源列表（例如，在`sources.js`文件中）中，可以将`forceflash`设置为`true`。 例如：

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

