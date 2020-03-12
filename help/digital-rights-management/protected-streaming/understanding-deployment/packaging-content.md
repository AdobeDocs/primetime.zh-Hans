---
description: 打包内容时，必须指定许可证服务器URL。
seo-description: 打包内容时，必须指定许可证服务器URL。
seo-title: 打包内容
title: 打包内容
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 打包内容{#packaging-content}

打包内容时，必须指定许可证服务器URL。

Adobe Primetime DRM Server URL采用以下格式：

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

例如，对于监听端口8080的许可证服务器主机名 `mylicenseserver.com` ，以及名为租户的许可证服务器主机名 *`tenant1`*，您应对于打包内容时指定的许可证服务器URL使用以下语法：

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

如果每个租户使用不同的许可证服务器和传输凭证，请确保在包装器中指定正确的租户证书。

如果要确保服务器仅向来自已知打包程序的内容颁发许可证，您需要将打包程序证书包含在租户配置文件的打包程序白名单中。
