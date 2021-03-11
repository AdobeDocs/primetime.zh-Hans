---
description: 打包内容时，必须指定许可证服务器URL。
title: 打包内容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# 正在打包内容{#packaging-content}

打包内容时，必须指定许可证服务器URL。

Adobe Primetime DRM服务器URL使用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，对于监听端口8080的许可证服务器主机名`mylicenseserver.com`和名为&#x200B;*`tenant1`*&#x200B;的租户，您应对在打包内容时指定的许可证服务器URL使用以下语法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每个租户使用不同的许可证服务器和传输凭据，请确保在打包程序中指定正确的租户证书。

如果要确保服务器仅向来自已知打包程序的内容颁发许可证，您需要将打包程序证书包含在租户配置文件的打包程序允许列表中。
