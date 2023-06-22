---
description: 使用可选的pttrackingmode、pttrackingversion和pttrackingposition查询参数获取URL，以将有关当前视频的广告跟踪信息发送到该URL。 响应因跟踪版本以及视频流是实时还是按需(VOD)而异。
title: 用于播放器与清单服务器交互的API
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 用于播放器与清单服务器交互的API {#api-for-players-to-interact-with-the-manifest-server}

使用可选 `pttrackingmode`， `pttrackingversion`、和 `pttrackingposition` 查询参数以获取要向其发送有关当前视频的广告跟踪信息的URL。 响应因跟踪版本以及视频流是实时还是按需(VOD)而异。

## 查询参数 {#query-parameters}

**pttrackingmode**

示例： `pttrackingmode=simple`
指定simple可告知清单服务器您需要跟踪信息。
在请求获取跟踪信息之前，在请求中指定它，以获取M3U8。如果未指定，清单服务器将在#EXT-X-MARKER标记中返回跟踪信息。
或者，如果您指定了简单值以外的有效值，则会调用服务器端跟踪。

**pttrackingversion**

示例： `pttrackingversion=v2`
此参数可告知清单服务器用于返回跟踪信息的格式(请参阅 [文件格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。
在请求获取跟踪信息之前，在请求中指定该值，以获取M3U8。如果未指定该值，或指定的值无效，则清单服务器将使用v1。

**pttrackingposition**

示例： `pttrackingposition`
此参数可告知清单服务器在M3U8文件中以JSON或VMAP对象的形式返回视频的跟踪信息。清单服务器会忽略指定的值，并发送其针对该会话拥有的所有跟踪信息。 如果未传递任何值，清单服务器将返回所请求的M3U8文件。
