---
description: 源列表中的forceflash标志强制Flash回退URL。 对于此URL，您可以使用Adobe Flash Player播放内容。
seo-description: 源列表中的forceflash标志强制Flash回退URL。 对于此URL，您可以使用Adobe Flash Player播放内容。
seo-title: 使用媒体源列表强制Flash回退
title: 使用媒体源列表强制Flash回退
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用媒体源列表强制Flash回退{#forcing-the-flash-fallback-using-the-media-source-list}

源列表中的forceflash标志强制Flash回退URL。 对于此URL，您可以使用Adobe Flash Player播放内容。

在媒体源列表(例如，在文 `sources.js` 件中)中，可以设置 `forceflash` 为 `true`。 例如：

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

