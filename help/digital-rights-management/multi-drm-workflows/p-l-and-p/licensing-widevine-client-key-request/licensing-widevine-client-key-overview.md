---
description: 若要播放内容打包产生的DASH内容，TVSDK客户端需要获取在密钥获取工作流中打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可证服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子交付给客户端。
title: 客户端密钥请求工作流概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 客户端密钥请求工作流{#client-key-request-workflow-overview}

若要播放内容打包产生的DASH内容，TVSDK客户端需要获取在密钥获取工作流中打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可证服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子交付给客户端。

要获取内容解密密钥，PSDK客户端必须执行以下操作

* 获取内容的pssh框，将其提供给平台，并获得响应密钥请求。
* 通过HTTPPOST将密钥请求发送到相应的Widevine/PlayReady许可证服务器。
* 将服务器的响应传递给平台，该平台将从响应中提取客户端内容解密密钥并将其用于内容解密。

要发出密钥请求的HTTPPOST，您的代码必须将许可证服务器URL连同任何需要附加到帖子的额外数据传递给PSDK客户端。 要传递的URL和数据的选择取决于您使用的Widevine/PlayReady服务提供商。 例如，如果您使用ExpressPlay提供服务，请传入相应的ExpressPlay Widevine/PlayReady许可证服务器URL，并附加到传出密钥请求中与内容的加密密钥关联的ExpressPlay令牌。 您可以从ExpressPlay文档获取相应的ExpressPlay WideIne/PlayReady许可证服务器URL。