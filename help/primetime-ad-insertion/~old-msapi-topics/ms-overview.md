---
description: 清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收客户端视频播放器从内容提供者接收的M3U8编码播放列表（清单），将来自广告提供商的广告拼接到清单中，并将拼接清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。
seo-description: 清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收客户端视频播放器从内容提供者接收的M3U8编码播放列表（清单），将来自广告提供商的广告拼接到清单中，并将拼接清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。
seo-title: 清单服务器交互概述
title: 清单服务器交互概述
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# 清单服务器交互{#overview-of-manifest-server-interactions}概述

清单服务器协调提供内容、提供广告、播放视频和跟踪广告的系统。 它接收客户端视频播放器从内容提供者接收的M3U8编码播放列表（清单），将来自广告提供商的广告拼接到清单中，并将拼接清单传递给视频播放器。 它支持客户端和服务器端广告跟踪。 它使用基于HTTP的Web服务界面进行交互。

典型配置包含：

* Primetime清单服务器
* Primetime创意重新打包服务(CRS)
* 控制视频播放器的客户端
* 发行商，通常带有内容管理系统(CMS)
* 内容投放网络(CDN)
* 广告服务器
* 广告跟踪报告的接收器

工作流程因多种因素而异，如CDN是Akamai还是客户端正在执行广告跟踪。 有关客户端广告跟踪工作流的示意图，请参阅[客户端跟踪工作流](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow)。

清单服务器通过接收和响应HTTP投放请求与视频GET客户端交互。 这些响应是描述广告拼接内容的M3U8编码清单，可选地包括包含详细广告跟踪说明的JSON或VMAP结构(sidecar)（请参阅[文件格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)）。

典型的工作流如下所示：

1. 发布者将广告服务器的内容URL和信息发送给客户端。
1. 客户端使用发布者提供的信息生成清单服务器URL并向该URL发送GET请求。 这称为BootstrapURL。
1. 清单服务器与客户端建立会话。
1. 清单服务器从CDN获得内容清单，其中可能包括广告中断信息。
1. 清单服务器将客户机重定向到为客户机生成的主控/变型清单。

   >[!NOTE]
   >
   >如果BootstrapURL查询参数包含`pttrackingmode=simple`或`ptplayer=ios-mobileweb`设置，清单服务器将返回JSON对象中的主控/变型清单URL，客户端将向该变型清单URL发送GET请求。

1. 客户端选择生成的变型清单中的流来播放，向清单服务器发送广告信息。
1. 清单服务器将客户端提供的信息传递给广告服务器，并从广告服务器接收广告和广告跟踪URL。 如果提供的广告不是HLS格式，清单服务器会将其发送到CRS以转换到HLS。
1. 清单服务器将广告拼接到内容清单中，并将新的拼接清单发送给客户。
1. 客户端使用拼接广告播放内容，并在指定的时间请求指定的跟踪URL。

Primetime广告插入支持许多视频投放平台上的客户。 并非所有客户端都以Primetime TVSDK包为构建基础，但所有客户端都将GET请求发送到相同的基本URL。 查询参数通过告诉清单服务器区分一个客户机请求和另一个客户机请求：

* 客户提出请求，
* 客户想要什么，
* 以及要提供的广告跟踪信息。

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

清单服务器使用跨来源资源共享标准(CORS)。 它在收到的请求中查找`Origin`头。 如果标题存在，则它会

* `Access-Control-Allow-Origin: *`来源标题中的字符串`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

如果没有，它将回复：

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`