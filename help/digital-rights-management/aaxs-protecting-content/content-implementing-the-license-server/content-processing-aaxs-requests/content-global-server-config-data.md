---
seo-title: 全局服务器配置数据
title: 全局服务器配置数据
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置之外，还存 `HandlerConfiguration` 储可发送到客户端以控制如何实施许可证的配置信息。 这是通过创建类并调用 `ServerConfigData` 来完成的( `HandlerConfiguration.setServerConfigData()` 这些设置仅适用于此许可证服务器颁发的许可证)。 时钟回退容差是许可证服务器可以设置的一个属性，用于控制客户端执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将计算机时钟回退4小时。 如果许可证服务器操作员希望使用其他设置，则可以在类中设置新 `ServerConfigData` 值。 当您更改其中任何设置的值时，请务必通过调用来增加版本号 `setVersion()`。 只有当客户端上的版本低于当前版本时，新值才会发送到客 `ServerConfigData` 户端。
