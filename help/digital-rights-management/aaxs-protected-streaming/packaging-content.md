---
seo-title: 打包内容
title: 打包内容
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 正在打包内容{#packaging-content}

打包内容时，必须指定许可证服务器URL。 Adobe Access ServerURL的格式为：

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

例如，对于在端口8080上侦听的许可证服务器主机名“mylicenseserver.com”和名为“tenant1”的租户，在打包时要指定的许可证服务器URL为：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每个租户使用不同的许可证服务器和传输凭据，请确保在打包程序中指定正确的租户证书。

要确保服务器仅向由已知打包程序打包的内容颁发许可证，请将打包程序的证书包含在租户配置文件的打包程序允许列表中。
