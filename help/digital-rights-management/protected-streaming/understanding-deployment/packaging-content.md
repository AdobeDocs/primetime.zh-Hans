---
description: 打包内容时，必须指定许可证服务器URL。
title: 打包内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 打包内容{#packaging-content}

打包内容时，必须指定许可证服务器URL。

Adobe Primetime DRM服务器URL使用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，对于许可证服务器主机名 `mylicenseserver.com` 监听端口8080，一个叫作 *`tenant1`*，您将为打包内容时指定的许可证服务器URL使用以下语法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每个租户使用不同的许可证服务器和传输凭据，请确保在打包程序中指定正确的租户证书。

如果要确保服务器仅向已知打包程序中的内容颁发许可证，您需要将打包程序的证书包含在租户配置文件的打包程序允许列表中。
