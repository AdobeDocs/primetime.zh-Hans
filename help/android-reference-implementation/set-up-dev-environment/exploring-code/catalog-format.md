---
description: Primetime参考实施使用基于JSON的信息源格式进行响应。 此格式使用IFeedItemAdapter接口的实现来解析。
title: 目录格式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 目录格式 {#catalog-format}

Primetime参考实施使用基于JSON的信息源格式进行响应。 此格式使用IFeedItemAdapter接口的实现来解析。

>[!NOTE]
>
>此信息源格式是参考实施使用的示例格式，可充当有关如何分析该格式并将其映射到信息源界面的示例。 您可以将自己的输入信息源格式用于自己的信息源界面实施。

从较高层面看，格式由一系列内容条目组成。 每个条目表示实时或VOD发布的视频内容：

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

每个馈送条目都是一个具有给定属性集的JSON对象：

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

| 属性 | 描述 |
|---|---|
| `id` | 信息源发布系统设置的内容的唯一标识符/指南。 |
| `title` | 内容的标题。 |
| `description` | 内容的描述。 |
| `categories` | 为内容标记的类别的列表，应用程序可以使用该列表来增强用户体验。 阅读内容的属性。 |
| `keywords` | 以逗号分隔的关键字列表，应用程序可以使用它来增强用户体验。 阅读内容的属性。 |
| `isLive` | true或false，指示它是Live流还是VOD流。 |
| `content` | JSON对象数组，具有内容的替代格式以及相应的URL。 例如，可以有f4m和m3u8格式的url。 JSON对象属性将在下面进行详细描述。 |
| `thumbnails` | JSON对象数组，其中包含不同大小缩略图的URL。 JSON对象属性定义如下。 |
| `metadata` | 为内容定义元数据的JSON对象，当前此元数据仅限于与广告相关的元数据。 元数据对象定义如下。 |

以下代码块定义了构成数组的JSON对象 **内容对象**：

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

| 属性 | 描述 |
|--- |--- |
| 格式 | 需要为Android的m3u8格式。 |
| url | 给定格式的视频流的URL。 |

以下代码块定义了构成数组的JSON对象 **缩略图对象**：

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

| 属性 | 描述 |
|---|---|
| 格式 | 一个字符串，指示缩略图文件的格式，例如JPEG、PNG等。 |
| 高度 | 缩略图的高度。 在参考应用程序中，具有最小高度和宽度的缩略图作为小缩略图返回，具有最大宽度和高度的缩略图作为大缩略图返回。 |
| 宽度 | 缩略图的宽度。 在参考应用程序中，具有最小高度和宽度的缩略图作为小缩略图返回，具有最大宽度和高度的缩略图作为大缩略图返回。 |
| url | 缩略图文件的url。 |

以下代码块定义 **元数据对象**：

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

| 属性 | 描述 |
|--- |--- |
| 广告 | 与广告相关的元数据。 |
| type | 值可以是Primetime广告、直接广告时间或自定义广告标记。 <br/><br/>PSDK为以下元数据类型提供内置支持：适用于Primetime广告服务（Primetime广告）的Auditude相关元数据、具有广告URL的直接广告时间（直接广告时间）以及为每个广告标记提供TimeRange的自定义广告标记（自定义广告标记）。 每种类型在PSDK中都有一个内置的AdProvider，用于处理元数据。  <br/><br/>下面定义了其中每个的JSON格式。 |
| 详细信息 | 包括广告元数据属性。 这两种类型的广告元数据都有其自己的一组属性，定义如下。 对于内置类型，包含的属性定义PSDK期望该类型的数据。 |
| 权利 | 与权利相关的元数据 |
| id | 用于针对Adobe Primetime pay-TV pass服务的授权请求的媒体资源ID。 ID可以是文本字符串或HTML编码的mRSS字符串。 任何需要授权的媒体内容都必须包含有效的资源ID。 |
