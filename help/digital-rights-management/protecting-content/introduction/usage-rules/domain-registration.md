---
title: 设备组域注册
description: 设备组域注册
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 设备组域注册{#device-group-domain-registration}

作为将许可证绑定到特定设备的替代方法，Primetime DRM 3.0或更高版本支持将许可证绑定到设备域。

多个设备可以加入域并接收域令牌。 在域中的设备获得许可证之后，许可证可以被转移到域中的任何其他设备，这些设备可以播放内容而无需直接从许可证服务器获得许可证。

如果您希望支持任何域绑定的许可证，则Primetime DRM策略必须指定客户端必须注册的域服务器。 Primetime DRM策略还必须指定域服务器的身份验证要求，无论是启用匿名访问，还是服务器需要用户名/密码还是自定义身份验证。

Primetime DRM客户端版本3.0或更高版本支持域注册和域绑定许可证。 如果Flash Player中较旧的客户端或Adobe Primetime 3.0客户端请求支持域注册的内容的许可证，则许可证服务器可能会颁发使用替代Primetime DRM策略支持绑定到特定设备的许可证。
