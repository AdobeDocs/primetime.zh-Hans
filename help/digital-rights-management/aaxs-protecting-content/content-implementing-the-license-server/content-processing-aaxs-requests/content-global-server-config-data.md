---
seo-title: 全局服务器配置数据
title: 全局服务器配置数据
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置外，`HandlerConfiguration`还存储可发送到客户端以控制如何实施许可证的配置信息。 这是通过创建`ServerConfigData`类并调用`HandlerConfiguration.setServerConfigData()`（这些设置仅适用于此许可证服务器颁发的许可证）来完成的。 时钟回退容限是许可证服务器可以设置的一个属性，用于控制客户端执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将计算机时钟设置回4小时。 如果许可证服务器操作员希望使用其他设置，可以在`ServerConfigData`类中设置新值。 当您更改任何这些设置的值时，请务必通过调用`setVersion()`来增加版本号。 只有当客户端上的版本小于当前的`ServerConfigData`版本时，新值才会发送到客户端。
