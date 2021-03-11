---
description: Primetime参考实施使用基于JSON的源格式进行响应。 使用IFeedItemAdapter接口的实现分析此格式。
title: 目录格式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# 目录格式{#catalog-format}

Primetime参考实施使用基于JSON的源格式进行响应。 使用IFeedItemAdapter接口的实现分析此格式。

>[!NOTE]
>
>此源格式是引用实现使用的示例格式，并作为如何分析格式并将其映射到源接口的示例。 您可以将自己的输入源格式与自己的源接口实现一起使用。

在高级别上，格式由一组内容条目组成。 每个条目表示实时或VOD发布的视频内容：

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

每个源条目都是具有一组给定属性的JSON对象：

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| 属性 | 说明 |
|---|---|
| `id` | 由源发布系统设置的内容的唯一标识符/指南。 |
| `title` | 内容的标题。 |
| `description` | 内容的描述。 |
| `categories` | 一列表类别标记为内容，该内容可由应用程序用来增强用户体验。 阅读内容的属性。 |
| `keywords` | 一列表以逗号分隔的关键字，可供应用程序使用以增强用户体验。 阅读内容的属性。 |
| `isLive` | true或false，指示它是实时流还是VOD流。 |
| `content` | JSON对象的数组，其中包含内容的替代格式以及相应的URL。 例如，f4m和m3u8格式可能有url。 JSON对象属性将在下面进一步说明。 |
| `thumbnails` | JSON对象的数组，其URL适用于不同大小的缩略图。 JSON对象属性在下面定义。 |
| `metadata` | 定义内容元数据的JSON对象，当前此元数据仅限于广告相关元数据。 元数据对象在下面定义。 |

以下代码块定义了构成&#x200B;**内容对象**&#x200B;数组的JSON对象：

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| 属性 | 说明 |
|--- |--- |
| 格式 | 对于Android，需要为m3u8格式。 |
| url | 给定格式的视频流的url。 |

以下代码块定义了构成&#x200B;**缩略图对象**&#x200B;数组的JSON对象：

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| 属性 | 说明 |
|---|---|
| 格式 | 一个字符串，指示缩览图文件的格式，例如JPEG、PNG等。 |
| 高 | 缩略图的高度。 在引用应用程序中，高度和宽度最小的缩略图作为小缩略图返回，宽度和高度最大的缩略图作为大缩略图返回。 |
| 宽度 | 缩略图的宽度。 在引用应用程序中，高度和宽度最小的缩略图作为小缩略图返回，宽度和高度最大的缩略图作为大缩略图返回。 |
| url | 缩略图文件的URL。 |

以下代码块定义&#x200B;**元数据对象**:

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| 属性 | 说明 |
|--- |--- |
| ad | 广告相关元数据。 |
| 类型 | 价值可以是Primetime广告、直接广告分段或自定义广告标记。 <br/><br/>PSDK为以下类型的元数据提供内置支持：Primetime广告投放（Primetime广告）的Auditude相关元数据、带有广告URL的直接广告分段（直接广告分段）以及为每个广告标记提供TimeRange的自定义广告标记（自定义广告标记）。每种类型在PSDK中都有一个内置的AdProvider，用于处理元数据。  <br/><br/>以下定义了每种JSON格式。 |
| 详细信息 | 包括广告元数据属性。 这两种类型的广告元数据都有其自己的属性集，定义如下。 对于内置类型，包含的属性定义PSDK预期的该类型数据。 |
| 权利 | 与授权相关的元数据 |
| id | 用于针对Adobe Primetime付费电视通行证服务进行授权请求的媒体资源ID。 该ID可以是文本字符串或HTML编码的mRSS字符串。 任何需要授权的媒体内容都必须包含有效的资源ID。 |

