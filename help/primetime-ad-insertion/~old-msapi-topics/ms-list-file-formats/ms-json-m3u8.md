---
description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，清单服务器将返回一个JSON格式的文件，其中包含主控M3U8，这是客户端用于请求描述内容的M3U8文件的URL。
seo-description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，清单服务器将返回一个JSON格式的文件，其中包含主控M3U8，这是客户端用于请求描述内容的M3U8文件的URL。
seo-title: 用于请求变型清单播放列表的URL的JSON格式
title: 用于请求变型清单播放列表的URL的JSON格式
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 请求变型清单播放列表{#json-format-for-url-for-requesting-variant-manifest-playlist}的URL的JSON格式

如果`pttrackingmode=simple`或`ptplayer=ios-mobileweb`，清单服务器将返回一个JSON格式的文件，其中包含主控M3U8，这是客户端用于请求描述内容的M3U8文件的URL。

这是包含`Master-M3U8` URL的JSON文件的格式。

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
