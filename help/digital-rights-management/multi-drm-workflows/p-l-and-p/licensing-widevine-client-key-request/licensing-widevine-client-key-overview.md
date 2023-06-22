---
description: 要播放内容打包产生的DASH内容，TVSDK客户端将需要获取在密钥获取工作流的打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可证服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子而传送到客户端。
title: 客户端密钥请求工作流概述
exl-id: ae600cbd-415b-441a-bf01-f259993071f2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 客户端密钥请求工作流 {#client-key-request-workflow-overview}

要播放内容打包产生的DASH内容，TVSDK客户端将需要获取在密钥获取工作流的打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可证服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子而传送到客户端。

要获取内容解密密钥，PSDK客户端必须执行以下操作

* 获取内容的pssh框，将其提供给平台，并获取密钥请求作为响应。
* 通过HTTPPOST将密钥请求发送到相应的Widevine/PlayReady许可证服务器。
* 将服务器的响应传递给平台，平台将从响应中提取客户端内容解密密钥，并将其用于内容解密。

要发送密钥请求的HTTPPOST，您的代码必须将许可证服务器URL以及需要附加到帖子的任何额外数据传递到PSDK客户端。 要传递的URL和数据选择取决于您所合作的Widevine/PlayReady服务提供商。 例如，如果使用ExpressPlay提供服务，则需传入相应的ExpressPlay Widevine/PlayReady许可证服务器URL，并将与内容加密密钥关联的ExpressPlay令牌附加到传出密钥请求。 您可以从ExpressPlay文档获取相应的ExpressPlay Widevine/PlayReady许可证服务器URL。
