---
description: 对于熟悉AdobePrimetime Access DRM解决方案的用户，Access和Primetime Cloud DRM之间有一些基本的架构差异，Primetime Cloud DRM由ExpressPlay解决方案提供支持。
seo-description: 对于熟悉AdobePrimetime Access DRM解决方案的用户，Access和Primetime Cloud DRM之间有一些基本的架构差异，Primetime Cloud DRM由ExpressPlay解决方案提供支持。
seo-title: 从访问迁移到多DRM
title: 从访问迁移到多DRM
uuid: 3e33ca9a-867e-46b8-bf88-8dbfe14ff786
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# 从访问迁移到多DRM {#migrating-from-access-to-multi-drm}

对于熟悉AdobePrimetime Access DRM解决方案的用户，Access和Primetime Cloud DRM之间有一些基本的架构差异，Primetime Cloud DRM由ExpressPlay解决方案提供支持。

## 多DRM与Access的体系结构差异

|  | 访问 | 多DRM |
|---|---|---|
| **打包** | Packager绑定到许可证服务器。 打包程序在打包内容时必须知道许可证服务器的公钥。 | Packager未绑定到一个许可证服务器。 |
|  | 内容打包后，即绑定到特定的许可证服务器。 | 内容未绑定到特定的许可证服务器。 其效果之一是，您可以在获得生产许可证之前将所有内容打包。 |
|  | Packager无需与任何形式的密钥存储进行通信，因为密钥经过加密后安全地嵌入到内容本身（元数据中）中。 只有相应的许可证服务器才能读取它们。 | 密钥必须从密钥存储系统发送&#x200B;*到*&#x200B;打包程序，或从&#x200B;*打包程序发送到密钥存储系统。*&#x200B;关键存储系统可以是客户自己的系统，也可以是ExpressPlay的关键存储。 |
| **授权** | 客户端向Access Cloud服务请求内容。 然后，Access云服务会向客户的授权系统发出请求。 客户的授权系统以客户的授权进行回复。 （在发出许可证请求之前，客户端可能已从客户的服务器获得一个用于登录的cookie。） | 客户端从客户的店面请求令牌（这可能是客户之前获得身份验证cookie的相同工作流）。 此时，客户执行授权检查。 如果授权检查通过，客户将向ExpressPlay服务器发送请求，为客户生成令牌。 此令牌始终绑定到特定内容，*可以*&#x200B;绑定到特定设备。 客户的店面将令牌发回给客户。 当客户端发出DRM播放请求时，该令牌将包含在请求中（此方法特定于设备），而ExpressPlay的DRM服务器验证令牌而不调用客户服务器。 |