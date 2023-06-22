---
title: 全局服务器配置数据
description: 全局服务器配置数据
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置外， `HandlerConfiguration` 存储可以发送到客户端的配置信息，以控制许可证的实施方式。 这是通过创建 `ServerConfigData` 类和调用 `HandlerConfiguration.setServerConfigData()`. 这些设置仅适用于此许可证服务器颁发的许可证。

时钟回溯容限是许可证服务器可以设置的一个属性，用于控制客户端强制执行许可证的方式。 默认情况下，用户可以将其计算机时钟向后设置4小时，而不会使许可证失效。 如果许可证服务器操作员希望使用其他设置，则可以在以下位置设置新值： `ServerConfigData` 类。 在更改其中任何设置的值时，请确保通过调用递增版本号 `setVersion()`. 仅当客户端上的版本比当前版本旧时，才会向客户端发送新值 `ServerConfigData` 版本。
