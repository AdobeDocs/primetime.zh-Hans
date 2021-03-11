---
description: 对于熟悉Adobe Primetime Access DRM解决方案的用户，Access和由ExpressPlay解决方案提供支持的Primetime Cloud DRM之间有一些基本的架构差异。
title: 从访问迁移到多DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 从访问迁移到多DRM {#migrating-from-access-to-multi-drm}

对于熟悉Adobe Primetime Access DRM解决方案的用户，Access和由ExpressPlay解决方案提供支持的Primetime Cloud DRM之间有一些基本的架构差异。

## 多DRM与访问的体系结构差异

|  | 访问 | 多DRM |
|---|---|---|
| **打包** | Packager绑定到许可证服务器。 打包程序在打包内容时必须知道许可证服务器的公钥。 | Packager不绑定到一个许可证服务器。 |
|  | 打包内容后，它将绑定到特定的许可证服务器。 | 内容未绑定到特定的许可证服务器。 其中一种效果是，您可以在获得生产许可证之前将所有内容打包。 |
|  | Packager无需与任何形式的密钥存储进行通信，因为密钥经过加密后安全地嵌入到内容本身（元数据中）中。 只有相应的许可证服务器才能读取它们。 | 密钥必须从密钥存储系统发送&#x200B;*到*&#x200B;打包程序，或从&#x200B;*打包程序发送到密钥存储系统。*&#x200B;关键存储系统可以是客户自己的系统，也可以是ExpressPlay的关键存储。 |
| **授权** | 客户端向Access Cloud服务请求内容。 然后，Access云服务会向客户的授权系统发出请求。 客户的授权系统以客户的授权作为回应。 （在发出许可证请求之前，客户端可能已从客户的服务器获得了一个Cookie以供登录。） | 客户端从客户的店面请求令牌（这可能是客户之前获取身份验证Cookie的相同工作流）。 此时，客户将执行授权检查。 如果授权检查通过，客户将向ExpressPlay服务器发送请求，以为客户生成令牌。 此令牌始终绑定到特定内容片段，*可以*&#x200B;绑定到特定设备。 客户的商店将令牌发回给客户。 当客户端发出DRM播放请求时，令牌将包含在请求中（这种方法是特定于设备的），而ExpressPlay的DRM服务器验证令牌而不调用客户服务器。 |