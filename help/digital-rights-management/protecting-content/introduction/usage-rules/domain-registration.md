---
seo-title: 设备组域注册
title: 设备组域注册
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 设备组域注册{#device-group-domain-registration}

作为将许可证绑定到特定设备的替代方法，Primetime DRM 3.0或更高版本支持将许可证绑定到设备域。

多个设备可以加入域并接收域令牌。 在域中的设备获得许可证后，许可证可以被传输到域中的任何其他设备，这些设备可以播放内容而无需直接从许可证服务器获取许可证。

如果要支持任何域绑定许可证，则Primetime DRM策略必须指定客户端必须注册的域服务器。 Primetime DRM策略还必须指定域服务器的身份验证要求，无论是启用匿名访问，还是服务器需要用户名／密码还是自定义身份验证。

Primetime DRM客户端版本3.0或更高版本支持域注册和域绑定许可证。 如果Flash Player中较旧的客户端或Adobe Primetime 3.0客户端请求支持域注册的内容的许可证，则许可证服务器可能会发出一个许可证，该许可证使用替代的Primetime DRM策略来支持绑定到特定设备。
