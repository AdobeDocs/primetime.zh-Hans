---
description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，清单服务器会发送回一个JSON格式的文件，其中包含Master-M3U8，这是客户端用于请求描述内容的M3U8文件的URL。
seo-description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，清单服务器会发送回一个JSON格式的文件，其中包含Master-M3U8，这是客户端用于请求描述内容的M3U8文件的URL。
seo-title: 用于请求变体清单播放列表的URL的JSON格式
title: 用于请求变体清单播放列表的URL的JSON格式
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 用于请求变体清单播放列表的URL的JSON格式 {#json-format-for-url-for-requesting-variant-manifest-playlist}

如果 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb`，清单服务器会发回一个JSON格式的文件，其中包含Master-M3U8，这是一个URL，客户端可使用它请求描述内容的M3U8文件。

这是包含URL的JSON文件的格 `Master-M3U8` 式。

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
