---
description: 源列表中的forceflash标志强制Flash回退URL。 对于此URL，您可以使用AdobeFlash Player播放内容。
seo-description: 源列表中的forceflash标志强制Flash回退URL。 对于此URL，您可以使用AdobeFlash Player播放内容。
seo-title: 使用媒体源Flash强制列表回退
title: 使用媒体源Flash强制列表回退
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 1%

---


# 使用媒体源Flash{#forcing-the-flash-fallback-using-the-media-source-list}强制列表回退

源列表中的forceflash标志强制Flash回退URL。 对于此URL，您可以使用AdobeFlash Player播放内容。

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

