---
description: 清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收客户端视频播放器从内容提供商接收的M3U8编码播放列表（清单），将广告提供商的广告拼接到清单中，并将拼接的清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。
title: 清单服务器交互概述
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# 清单服务器交互概述 {#overview-of-manifest-server-interactions}

清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收客户端视频播放器从内容提供商接收的M3U8编码播放列表（清单），将广告提供商的广告拼接到清单中，并将拼接的清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。

典型配置包含：

* Primetime清单服务器
* Primetime Creative Repackaging Service (CRS)
* 客户端，控制视频播放器
* 发布者，通常具有内容管理系统(CMS)
* 内容交付网络(CDN)
* 广告服务器
* 广告跟踪报表的接收者

工作流会因多种因素而异，例如CDN是否为Akamai，或者客户端是否正在执行广告跟踪。 有关客户端广告跟踪的工作流图表，请参阅 [客户端跟踪工作流](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

清单服务器通过接收和响应HTTPGET请求与视频交付客户端进行交互。 响应是描述广告拼接内容的M3U8编码清单，可选地包括包含详细广告跟踪指令的JSON或VMAP结构(sidecar)(请参阅 [文件格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。

典型的工作流如下所示：

1. 发布者将广告服务器的内容URL和信息发送到客户端。
1. 客户端使用来自发布者的信息生成清单服务器URL，并向该URL发送GET请求。 这称为BootstrapURL。
1. 清单服务器与客户端建立会话。
1. 清单服务器从CDN获取内容清单，其中可能包括广告时间信息。
1. 清单服务器将客户端重定向到它为客户端生成的主控/变体清单。

   >[!NOTE]
   >
   >如果BootstrapURL查询参数包含 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb` 设置时，清单服务器在JSON对象中返回主控/变体清单URL，客户端向该变体清单URL发送GET请求。

1. 客户端选择播放生成的变量清单中的流，将广告信息发送到清单服务器。
1. 清单服务器将客户端提供的信息传递到广告服务器，并从广告服务器接收广告和广告跟踪URL。 如果提供的广告不是HLS格式，则清单服务器会将其发送到CRS以转换为HLS。
1. 清单服务器将广告拼接到内容清单中，并将新拼接的清单发送到客户端。
1. 客户端播放带有拼接广告的内容，并在指定时间向指定的跟踪URL发出请求。

Primetime Ad Insertion支持许多视频交付平台上的客户端。 并非所有客户端都基于Primetime TVSDK包构建，但所有客户端都向同一基本URL发送GET请求。 查询参数通过告知清单服务器来区分一个客户端请求和另一个客户端请求：

* 哪个客户端发出请求，
* 客户想要什么，
* 以及要提供的广告跟踪信息。

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

清单服务器使用跨源资源共享标准(CORS)。 它查找 `Origin` 标头。 如果标头存在，则会回复

* `Access-Control-Allow-Origin: *`来自Origin标头的字符串`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

如果没有，它将回复为：

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`