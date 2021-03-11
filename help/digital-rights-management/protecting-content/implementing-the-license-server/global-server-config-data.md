---
title: 全局服务器配置数据
description: 全局服务器配置数据
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置之外，`HandlerConfiguration`还存储可发送到客户端以控制如何实施许可证的配置信息。 创建`ServerConfigData`类并调用`HandlerConfiguration.setServerConfigData()`即可完成此操作。 这些设置仅适用于此许可证服务器颁发的许可证。

时钟回退容差是许可证服务器可以设置的一个属性，用于控制客户端执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将计算机时钟设置回4小时。 如果许可证服务器操作员希望使用其他设置，则可以在`ServerConfigData`类中设置新值。 更改任何这些设置的值时，请务必通过调用`setVersion()`来增加版本号。 只有当客户端上的版本早于当前`ServerConfigData`版本时，新值才会发送到客户端。
