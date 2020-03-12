---
description: 清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收M3U8编码的播放列表（清单），客户视频播放器从内容提供商接收，将广告从广告提供商缝入清单，并将拼合清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。
seo-description: 清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收M3U8编码的播放列表（清单），客户视频播放器从内容提供商接收，将广告从广告提供商缝入清单，并将拼合清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。
seo-title: 清单服务器交互概述
title: 清单服务器交互概述
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: 9dc8498593a1d70918b66016e429eb013cdc61f7

---


# 清单服务器交互概述 {#overview-of-manifest-server-interactions}

清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收M3U8编码的播放列表（清单），客户视频播放器从内容提供商接收，将广告从广告提供商缝入清单，并将拼合清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。

典型配置包含：

* Primetime清单服务器
* Primetime Creative Repackaging Service(CRS)
* 控制视频播放器的客户端
* 发布者，通常带有内容管理系统(CMS)
* 内容交付网络(CDN)
* 广告服务器
* 广告跟踪报告的接收方

工作流程因诸多因素而异，如CDN是Akamai还是客户端正在执行广告跟踪。 有关客户端广告跟踪工作流的示意图，请参 [阅客户端跟踪工作流](../msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow)。

清单服务器通过接收和响应HTTP GET请求与视频交付客户端交互。 这些响应是描述广告拼接内容的M3U8编码清单，可选地包括包含详细广告跟踪说明的JSON或VMAP结构（附加项）(请参阅 [文件格式](../msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。

典型的工作流如下所示：

1. 发布者将广告服务器的内容URL和信息发送到客户端。
1. 客户端使用发布者提供的信息生成清单服务器URL并向该URL发送GET请求。 这称为引导URL。
1. 清单服务器与客户端建立会话。
1. 清单服务器从CDN获取内容清单，其中可能包括广告中断信息。
1. 清单服务器将客户机重定向到为客户机生成的主／变型清单。

   >[!NOTE]
   >
   >如果Bootstrap URL查询参数包含或设 `pttrackingmode=simple``ptplayer=ios-mobileweb` 置，则清单服务器会在JSON对象中返回主／变型清单URL，并且客户端会向该变型清单URL发送GET请求。

1. 客户端选择生成的变体清单中的流来播放，向清单服务器发送广告信息。
1. 清单服务器将客户端提供的信息传递给广告服务器，并从广告服务器接收广告和广告跟踪URL。 如果提供的广告不是HLS格式，清单服务器会将其发送到CRS，以便转换到HLS。
1. 清单服务器将广告拼接到内容清单中并将新的拼接清单发送到客户端。
1. 客户端使用拼合广告播放内容，并在指定时间向指定的跟踪URL发出请求。

Primetime广告插入支持许多视频交付平台上的客户。 并非所有客户端都以Primetime TVSDK包为构建基础，但所有客户端都将GET请求发送到相同的基本URL。 查询参数通过通知清单服务器区分一个客户机请求和另一个客户机请求：

* 哪个客户提出请求，
* 客户想要什么，
* 以及要提供的广告跟踪信息。

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

清单服务器使用跨源资源共享标准(CORS)。 它在收到的 `Origin` 请求中查找头。 如果标题存在，则它将回复

* `Access-Control-Allow-Origin: *`源标题中的字符串`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

如果没有，它将回复：

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`