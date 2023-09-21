---
title: 打包内容
description: 打包内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 打包内容{#packaging-content}

在打包远程密钥投放的内容时，请使用指定需要远程密钥投放的策略。 对于HLS内容，密钥服务器URL必须包含在M3U8（清单文件）中。 Primetime DRM密钥服务器URL的格式为：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，密钥服务器主机名 [!DNL mykeyserver.com] 在端口443上侦听，租户名为 `tenant1`，则在M3U8中指定的密钥服务器URL为：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS和Xbox 360客户端均可使用相同的URL。 或者，如果为服务器配置了每种客户端类型的单独租户，则可以使用不同的URL。

只要许可证服务器URL指向正确配置的运行许可证服务器，就可以在不需要密钥服务器的客户端上播放相同的内容。
