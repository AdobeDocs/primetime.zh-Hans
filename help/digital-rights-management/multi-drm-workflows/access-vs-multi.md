---
description: 对于熟悉Adobe Primetime Access DRM解决方案的用户，Access与ExpressPlay解决方案支持的Primetime Cloud DRM之间有一些基本的架构差异。
seo-description: 对于熟悉Adobe Primetime Access DRM解决方案的用户，Access与ExpressPlay解决方案支持的Primetime Cloud DRM之间有一些基本的架构差异。
seo-title: 从访问迁移到多DRM
title: 从访问迁移到多DRM
uuid: 3e33ca9a-867e-46b8-bf88-8dbfe14ff786
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 从访问迁移到多DRM {#migrating-from-access-to-multi-drm}

对于熟悉Adobe Primetime Access DRM解决方案的用户，Access与ExpressPlay解决方案支持的Primetime Cloud DRM之间有一些基本的架构差异。

## 访问与多DRM的体系结构差异

|  | 访问 | 多DRM |
|---|---|---|
| **打包** | Packager绑定到许可证服务器。 打包内容时，Packager必须知道许可证服务器的公钥。 | Packager未绑定到一个许可证服务器。 |
|  | 内容打包后，即绑定到特定的许可证服务器。 | 内容未绑定到特定的许可证服务器。 其一个效果是，您可以在获得生产许可证之前打包所有内容。 |
|  | Packager无需与任何形式的密钥存储进行通信，因为密钥经过加密后安全地嵌入到内容本身（元数据中）中。 只有相应的许可证服务器才能读取它们。 | 密钥必须从密 *钥存储系统发送到* Packager，或从Packager *发送* 到密钥存储系统。 密钥存储系统可以是客户自己的系统，也可以是ExpressPlay的密钥存储。 |
| **授权** | 客户端向Access Cloud服务请求内容。 然后，Access云服务向客户的授权系统发出请求。 客户的授权系统以客户的授权作为回应。 （在发出许可证请求之前，客户端可能已从客户的服务器获得一个Cookie进行登录。） | 客户端从客户的店面发出令牌请求（这可能与客户之前获得身份验证Cookie的工作流相同）。 此时，客户将执行授权检查。 如果授权检查通过，客户会向ExpressPlay服务器发送请求，为客户生成令牌。 此令牌始终绑定到特定内容片段，并 *且可能* 绑定到特定设备。 客户的店面将令牌发回给客户。 当客户端发出DRM播放请求时，令牌将包含在请求中（这是设备特定的方法），而ExpressPlay的DRM服务器验证令牌而不调用客户服务器。 |