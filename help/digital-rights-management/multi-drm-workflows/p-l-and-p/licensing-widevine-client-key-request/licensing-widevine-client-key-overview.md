---
description: 要播放内容打包产生的DASH内容，TVSDK客户端需要获取内容解密密钥，该密钥是在密钥获取工作流中打包过程中传递的。 客户端内容解密密钥通常由Widevine/PlayReady许可证服务器传送给客户端，以响应来自客户端的一个或多个HTTP/HTTPS帖子。
title: 客户端密钥请求工作流概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 客户端密钥请求工作流 {#client-key-request-workflow-overview}

要播放内容打包产生的DASH内容，TVSDK客户端需要获取内容解密密钥，该密钥是在密钥获取工作流中打包过程中传递的。 客户端内容解密密钥通常由Widevine/PlayReady许可证服务器传送给客户端，以响应来自客户端的一个或多个HTTP/HTTPS帖子。

要获取内容解密密钥，PSDK客户端必须执行以下操作

* 获取内容的pssh框，将其提供给平台，并获取密钥请求作为响应。
* 通过HTTPPOST将密钥请求发送到相应的Widevine/PlayReady许可证服务器。
* 将服务器的响应传递给平台，平台将从响应中提取客户端内容解密密钥，并将其用于内容解密。

要发送密钥请求的HTTPPOST，您的代码必须将许可证服务器URL以及需要附加到帖子的任何额外数据传递到PSDK客户端。 要传递的URL和数据选择取决于您所合作的Widevine/PlayReady服务提供商。 例如，如果使用ExpressPlay提供服务，则传入相应的ExpressPlay Widevine/PlayReady许可证服务器URL，并将与内容的加密密钥关联的ExpressPlay令牌附加到传出密钥请求。 您可以从ExpressPlay文档获取相应的ExpressPlay Widevine/PlayReady许可证服务器URL。
