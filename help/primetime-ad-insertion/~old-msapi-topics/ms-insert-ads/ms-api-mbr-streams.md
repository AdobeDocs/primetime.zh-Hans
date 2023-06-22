---
description: 广告插入的客户端请求通常在变体M3U8格式的播放列表中指定一个以上的比特率。 清单服务器生成并返回一个新的变体M3U8文件，该文件包含用于每个比特率的单独M3U8链接。 它还生成唯一的组ID以将这些M3U8绑定在一起。
title: 多比特率流
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 多比特率流 {#multiple-bit-rate-streams}

广告插入的客户端请求通常在变体M3U8格式的播放列表中指定一个以上的比特率。 清单服务器生成并返回一个新的变体M3U8文件，该文件包含用于每个比特率的单独M3U8链接。 它还生成唯一的组ID以将这些M3U8绑定在一起。

清单服务器使用客户端BootstrapURL请求中的信息来检索内容变体播放列表。 它生成一个新的变体播放列表，其中包含指向流级别内容的清单服务器链接。 客户端使用这些插件来构建广告插入请求。 清单服务器的流级别内容链接具有以下格式：

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 清单服务器根据内容的播放列表类型设置此值：实时/线性(#EXT-X-PLAYLIST-TYPE：EVENT)或VOD (#EXT-X-PLAYLIST-TYPE：VOD)

* **`publisherAssetID`** BootstrapURL请求中提供的特定内容的发布者唯一ID。

* **`rendition`** 清单服务器根据内容流的BANDWIDTH值设置此项，并使用它匹配广告的比特率与内容的比特率。 广告比特率不能超过内容的比特率，除非具有最低比特率的广告演绎版这样做。

* **`groupID`** 清单服务器会生成此值并使用它来确保无论客户端请求广告的位速率演绎版为何，都始终如一地放置广告。

* **`base64-encoded url of the bit rate stream`** 清单服务器URL安全的base64对内容流的绝对URL进行编码。 每个流都有自己的URL。

* **`Query parameters`** BootstrapURL请求中提供的查询参数。

