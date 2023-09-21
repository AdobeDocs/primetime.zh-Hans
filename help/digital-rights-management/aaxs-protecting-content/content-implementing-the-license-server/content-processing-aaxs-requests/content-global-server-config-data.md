---
title: 全局服务器配置数据
description: 全局服务器配置数据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置外， `HandlerConfiguration` 存储可以发送到客户端的配置信息，以控制许可证的实施方式。 这是通过创建 `ServerConfigData` 类和调用 `HandlerConfiguration.setServerConfigData()` （这些设置仅适用于此许可证服务器颁发的许可证）。 时钟回溯容限是许可证服务器可以设置的一个属性，用于控制客户端强制执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将其计算机时钟向后设置4小时。 如果许可证服务器操作员希望使用不同的设置，则可以在以下位置设置新值： `ServerConfigData` 类。 在更改其中任何设置的值时，请确保通过调用递增版本号 `setVersion()`. 仅当客户端上的版本小于当前版本时，才会将新值发送到客户端 `ServerConfigData` 版本。
