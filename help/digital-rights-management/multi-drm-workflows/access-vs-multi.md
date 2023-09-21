---
description: 对于那些熟悉Adobe的Primetime访问DRM解决方案的人来说，Access与由ExpressPlay解决方案提供支持的Primetime Cloud DRM之间存在一些根本性的体系结构差异。
title: 从访问迁移到多DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 从访问迁移到多DRM {#migrating-from-access-to-multi-drm}

对于那些熟悉Adobe的Primetime访问DRM解决方案的人来说，Access与由ExpressPlay解决方案提供支持的Primetime Cloud DRM之间存在一些根本性的体系结构差异。

## 访问与多DRM之间的体系结构差异

|  | 访问 | 多DRM |
|---|---|---|
| **包装** | Packager已绑定到许可证服务器。 打包内容时，Packager必须知道许可证服务器的公钥。 | Packager未绑定到一个许可证服务器。 |
|  | 内容一经打包，就会绑定到特定的许可证服务器。 | 内容未绑定到特定的许可证服务器。 其后果之一是，您可以在获取生产许可证之前打包所有内容。 |
|  | Packager不需要与任何形式的密钥存储进行通信，因为密钥在加密后安全地嵌入到内容本身（在元数据中）中。 只有相应的许可证服务器可以读取它们。 | 必须发送密钥 *到* 来自密钥存储系统的打包程序，或发送 *从* 密钥存储系统的打包程序。 密钥存储系统可以是客户自己的系统，也可以是ExpressPlay的密钥存储。 |
| **权利** | 客户端向Access Cloud服务请求内容。 然后，访问云服务会向客户的授权系统发出请求。 客户的授权系统用客户的授权进行响应。 （客户端在发出许可证请求之前，可能已经从客户的服务器获得了用于登录的Cookie。） | 客户端从客户的店面请求令牌（这可能与客户之前在其中获得身份验证Cookie的工作流相同）。 此时，客户执行权利检查。 如果授权检查通过，客户将向ExpressPlay服务器发送请求，以便为客户生成令牌。 此令牌始终绑定到特定内容，并且 *五月* 绑定到特定设备。 客户的店面将令牌发送回客户端。 当客户端发出DRM播放请求时，该令牌将包含在请求中（此方法特定于设备），并且ExpressPlay的DRM服务器将验证该令牌，而不调用客户的服务器。 |
