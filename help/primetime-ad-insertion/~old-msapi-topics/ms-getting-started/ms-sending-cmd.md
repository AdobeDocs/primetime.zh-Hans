---
description: 使用HTTPGET命令与清单服务器进行交互。
title: 向清单服务器发送命令
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 向清单服务器{#send-a-command-to-the-manifest-server}发送命令

使用HTTPGET命令与清单服务器进行交互。

1. 发送`HTTP GET`请求以使用以下模式构建的引导URL:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **需** 要PublisherAssetIDR。特定内容的发布者唯一ID。

* **内** 容URLRequired。内容M3U8文件的URL，Base64编码为在清单服务器URL中是安全的。 内容URL必须指向变体的M3U8文件，即使只有一个比特率流。

* **查询** 参数某些是必需的，某些是可选的。这些是请求中最多样的部分。 它们告诉清单服务器发出请求的客户机类型以及清单服务器希望做什么。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP与HTTPS请求**

   清单服务器使用客户端请求的相同HTTP协议创建URL。 如果播放器发出了非安全的HTTP(http)请求，清单服务器会使用http协议返回清单URL和Auditude跟踪URL。 如果播放器建立安全的HTTP(https)连接，清单服务器，则会返回具有https协议的清单URL和Auditude跟踪URL。

   >[!NOTE]
   >
   >清单服务器无法更改内容段(.ts)和第三方跟踪信标的协议（HTTP或HTTPS）。 您必须联系内容和第三方广告提供商，让他们配置所需的协议。