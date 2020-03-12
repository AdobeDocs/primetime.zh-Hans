---
description: 要播放由内容打包产生的DASH内容，TVSDK客户端需要获得在密钥获取工作流的打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子而交付给客户端。
seo-description: 要播放由内容打包产生的DASH内容，TVSDK客户端需要获得在密钥获取工作流的打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子而交付给客户端。
seo-title: 客户端密钥请求工作流概述
title: 客户端密钥请求工作流概述
uuid: 2f01f0ae-adbf-42fa-a908-4b5b9410a26d
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 客户端密钥请求工作流 {#client-key-request-workflow-overview}

要播放由内容打包产生的DASH内容，TVSDK客户端需要获得在密钥获取工作流的打包过程中传递的内容解密密钥。 客户端内容解密密钥通常由Widevine/PlayReady许可服务器响应于来自客户端的一个或多个HTTP/HTTPS帖子而交付给客户端。

要获取内容解密密钥，PSDK客户端必须执行以下操作

* 抓住内容的pssh框，将其提供给平台，并获取响应密钥请求。
* 通过HTTP POST将密钥请求发送到相应的Widevine/PlayReady许可证服务器。
* 将服务器的响应传递给平台，该平台将从响应中提取客户端内容解密密钥并将其用于内容解密。

要发出HTTP POST以发出密钥请求，您的代码必须将许可证服务器URL以及任何需要附加到帖子的额外数据传递给PSDK客户端。 要传递的URL和数据的选择取决于您所使用的Widevine/PlayReady服务提供商。 例如，如果您使用ExpressPlay提供服务，请传入相应的ExpressPlay Widevine/PlayReady许可证服务器URL，并附加到传出密钥请求中与内容的加密密钥关联的ExpressPlay令牌。 您可以从ExpressPlay文档获取相应的ExpressPlay Widevine/PlayReady许可证服务器URL。