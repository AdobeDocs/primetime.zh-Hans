---
description: 客户端广告插入请求通常在变体M3U8格式的播放列表中指定多个比特率。 清单服务器生成并返回一个新的变体M3U8文件，其中每个比特率包含一个单独的M3U8链接。 它还生成一个唯一的组ID来将这些M3U8绑定在一起。
title: 多比特率流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 多比特率流{#multiple-bit-rate-streams}

客户端广告插入请求通常在变体M3U8格式的播放列表中指定多个比特率。 清单服务器生成并返回一个新的变体M3U8文件，其中每个比特率包含一个单独的M3U8链接。 它还生成一个唯一的组ID来将这些M3U8绑定在一起。

清单服务器使用客户端的BootstrapURL请求中的信息来检索内容变体播放列表。 它生成一个新的变体播放列表，其中包含指向流级内容的清单服务器链接。 客户端使用它们来构建广告插入请求。 清单服务器的流级内容链接具有以下格式：

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 清单服务器根据内容的播放列表类型设置此值：实时/线性(#EXT-X-PLAYLIST-TYPE:事件)或VOD(#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** 针对在BootstrapURL请求中提供的特定内容的发布者的唯一ID。

* **`rendition`** 清单服务器根据内容流的BANDWIDTH值设置该值，并使用它将广告的比特率与内容的比特率匹配。除非具有最低比特率的广告再现超过内容的比特率，否则广告比特率不能超过内容的比特率。

* **`groupID`** 清单服务器生成此值并使用它来确保它一致地放置广告，而不管客户请求广告的哪个位速率再现。

* **`base64-encoded url of the bit rate stream`** 清单服务器URL安全base64对内容流的绝对URL进行编码。每个流都有其自己的URL。

* **`Query parameters`** 查询参数在BootstrapURL请求中提供。

