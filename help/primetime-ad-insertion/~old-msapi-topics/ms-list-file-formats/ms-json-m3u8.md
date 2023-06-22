---
description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，则清单服务器会发送回包含主控-M3U8的JSON格式的文件，该文件是客户端用于请求描述内容的M3U8文件的URL。
title: 用于请求变体清单播放列表的URL的JSON格式
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 用于请求变体清单播放列表的URL的JSON格式 {#json-format-for-url-for-requesting-variant-manifest-playlist}

如果 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb`，清单服务器会发送回包含主控M3U8的JSON格式的文件，客户端使用该URL来请求描述内容的M3U8文件。

这是包含的JSON文件的格式 `Master-M3U8` URL。

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
