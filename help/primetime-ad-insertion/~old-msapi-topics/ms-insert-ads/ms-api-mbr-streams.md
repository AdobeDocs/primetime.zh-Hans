---
description: 客户端广告插入请求通常在变型M3U8格式的播放列表中指定多个比特率。 清单服务器生成并返回一个新的变型M3U8文件，该文件包含每个比特率的单独的M3U8链路。 它还生成唯一的组ID来将这些M3U8绑定在一起。
seo-description: 客户端广告插入请求通常在变型M3U8格式的播放列表中指定多个比特率。 清单服务器生成并返回一个新的变型M3U8文件，该文件包含每个比特率的单独的M3U8链路。 它还生成唯一的组ID来将这些M3U8绑定在一起。
seo-title: 多比特率流
title: 多比特率流
uuid: f59cb765-e000-43e0-8d3a-8149a3c5b96e
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 多比特率流{#multiple-bit-rate-streams}

客户端广告插入请求通常在变型M3U8格式的播放列表中指定多个比特率。 清单服务器生成并返回一个新的变型M3U8文件，该文件包含每个比特率的单独的M3U8链路。 它还生成唯一的组ID来将这些M3U8绑定在一起。

清单服务器使用客户端的BootstrapURL请求中的信息来检索内容变体播放列表。 它生成一个新的变体播放列表，其中包含指向流级内容的清单服务器链接。 客户端使用这些请求来构建广告插入请求。 清单服务器的流级内容链接具有以下格式：

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 清单服务器根据内容的播放列表类型设置此值：实时／线性(#EXT-X-PLAYLIST-TYPE:VOD)或VOD(#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** BootstrapURL请求中提供的特定内容的发布者唯一ID。

* **`rendition`** 清单服务器根据内容流的BANDWIDT值设置此值，并使用它将广告的比特率与内容的比特率相匹配。除非具有最低比特率的广告再现超过内容的比特率，否则广告比特率不能超过内容的比特率。

* **`groupID`** 清单服务器生成此值并使用它来确保它始终如一地放置广告，无论客户请求广告的哪个比特率再现。

* **`base64-encoded url of the bit rate stream`** 清单服务器URL安全base64对内容流的绝对URL进行编码。每个流都有其自己的URL。

* **`Query parameters`** 查询URL请求中提供的Bootstrap参数。

