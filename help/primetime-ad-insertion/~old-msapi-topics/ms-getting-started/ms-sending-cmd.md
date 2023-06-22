---
description: 使用HTTPGET命令与清单服务器交互。
title: 向清单服务器发送命令
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 向清单服务器发送命令 {#send-a-command-to-the-manifest-server}

使用HTTPGET命令与清单服务器交互。

1. 发送 `HTTP GET` 请求使用以下模式构建的引导URL：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetID** 必需。 特定内容的发布者唯一ID。

* **内容URL** 必需。 内容M3U8文件的URL，在清单服务器URL中编码为安全的Base64。 内容URL必须指向变体M3U8文件，即使只有一个比特率流也是如此。

* **查询参数** 有些是必需的，有些是可选的。 这些构成了请求中最具多样性的部分。 它们告知清单服务器哪种客户端正在发出请求，以及它希望清单服务器做什么。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP与HTTPS请求**

   清单服务器使用客户端请求的相同HTTP协议创建URL。 如果播放器发出非安全HTTP (http)请求，则清单服务器会使用http协议返回清单URL和审核跟踪URL。 如果播放器建立了安全HTTP (https)连接、清单服务器，则会通过https协议返回清单URL和审核跟踪URL。

   >[!NOTE]
   >
   >清单服务器无法更改内容区段(.ts)和第三方跟踪信标的协议（HTTP或HTTPS）。 您必须联系内容和第三方广告提供商，以便他们配置所需的协议。