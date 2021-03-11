---
title: 打包内容
description: 打包内容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 正在打包内容{#packaging-content}

在打包内容以进行远程密钥投放时，请使用指定需要远程密钥投放的策略。 HLS内容的M3U8（清单文件）中必须包含密钥服务器URL。 Primetime DRM密钥服务器URL的格式为：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，对于侦听端口443的密钥服务器主机名[!DNL mykeyserver.com]和名为`tenant1`的租户，要在M3U8中指定的密钥服务器URL为：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

同一URL可用于iOS和Xbox 360客户端。 或者，如果服务器针对每种客户端类型配置了不同的租户，则可能使用不同的URL。

只要许可证服务器URL指向正确配置的运行许可证服务器，就可以在不需要密钥服务器的客户端上播放相同的内容。
