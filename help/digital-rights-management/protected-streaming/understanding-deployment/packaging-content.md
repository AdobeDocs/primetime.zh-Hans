---
description: 打包内容时，必须指定许可证服务器URL。
seo-description: 打包内容时，必须指定许可证服务器URL。
seo-title: 打包内容
title: 打包内容
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 打包内容{#packaging-content}

打包内容时，必须指定许可证服务器URL。

Adobe Primetime DRM Server URL采用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，对于监听端口 `mylicenseserver.com` 8080的许可证服务器主机名和名为租户 *`tenant1`*，您应该对打包内容时指定的许可证服务器URL使用以下语法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每个租户使用不同的许可证服务器和传输凭据，请确保在打包程序中指定正确的租户证书。

如果要确保服务器仅向已知打包程序的内容颁发许可证，您需要在打包程序允许租户配置文件列表中包含打包程序的证书。
