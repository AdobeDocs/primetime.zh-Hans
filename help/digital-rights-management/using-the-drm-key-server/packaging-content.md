---
seo-title: 打包内容
title: 打包内容
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# 打包内容{#packaging-content}

将内容打包以进行远程密钥交付时，请使用指定需要远程密钥交付的策略。 HLS内容的M3U8（清单文件）中必须包含密钥服务器URL。 Primetime DRM密钥服务器URL的格式为：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，对于在端口443上监 [!DNL mykeyserver.com] 听的密钥服务器主机名和名为租户的 `tenant1`,M3U8中要指定的密钥服务器URL是：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

同一URL可用于iOS和Xbox 360客户端。 或者，如果服务器针对每种客户端类型配置了不同的租户，则可能使用不同的URL。

只要许可证服务器URL指向正确配置的运行许可证服务器，就可以在不需要密钥服务器的客户端上播放相同的内容。
