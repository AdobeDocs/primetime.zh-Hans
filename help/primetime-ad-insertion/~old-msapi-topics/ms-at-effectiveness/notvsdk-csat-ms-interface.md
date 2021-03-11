---
description: 使用可选的pttrackingmode、pttrackingversion和pttrackingposition查询参数可获取要向其发送有关当前视频的广告跟踪信息的URL。 响应因跟踪版本以及视频流是实时的还是点播(VOD)而异。
title: 用于播放器与清单服务器交互的API
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 播放器与清单服务器{#api-for-players-to-interact-with-the-manifest-server}交互的API

使用可选的`pttrackingmode`、`pttrackingversion`和`pttrackingposition`查询参数可获取要向其发送有关当前视频的广告跟踪信息的URL。 响应因跟踪版本以及视频流是实时的还是点播(VOD)而异。

## 查询参数{#query-parameters}

**pttrackingmode**

示例：`pttrackingmode=simple`
指定“简单”会通知清单服务器您想要跟踪信息。
请在请求跟踪信息之前在请求中指定获取M3U8的请求。如果未指定，清单服务器将返回#EXT-X-MARKER标记中的跟踪信息。
或者，如果指定除简单之外的有效值，则调用服务器端跟踪。

**pttrackingversion**

示例：`pttrackingversion=v2`
此参数告知清单服务器要使用哪种格式返回跟踪信息（请参阅[文件格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)）。
请在请求跟踪信息之前在请求中指定它以获取M3U8。如果未指定它或指定无效值，则清单服务器将使用v1。

**pttrackposition**

示例：`pttrackingposition`
此参数告知清单服务器将视频的跟踪信息作为M3U8文件中的JSON或VMAP对象返回。清单服务器将忽略指定值并发送它为该会话拥有的所有跟踪信息。 如果未传递任何值，则清单服务器返回所请求的M3U8文件。
