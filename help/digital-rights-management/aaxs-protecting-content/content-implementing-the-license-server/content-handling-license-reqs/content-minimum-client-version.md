---
title: 最低客户端版本
description: 最低客户端版本
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 最低客户端版本{#minimum-client-version}

Adobe Access 2.0.2及更高版本引入了一些新的使用规则，而Adobe Access 2.0客户端不理解这些规则。 通过设置最低支持的客户端版本(`HandlerConfiguration.setMinSupportedClientVersion()`)，许可证服务器可以控制当旧客户端遇到具有这些使用规则的许可证时其行为。 根据此设置，服务器可以指示旧客户端是否可以忽略他们不了解的使用规则，或者旧客户端是否无法使用这些使用规则使用许可证。

例如，

* 如果许可证指定了设备功能要求（播放受保护内容所需的[设备功能](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)），则Adobe Access客户端2.0.2及更高版本可以执行这些要求。
* 如果许可证服务器不希望内容在不了解设备功能要求的客户端上播放，请将支持的最低客户端版本设置为2（对于2.0.2）。 这将阻止服务器在2.0.2之前向Adobe Access客户端发放许可证。如果许可证从一个客户端传输到另一个客户端，则还将强制使用最低客户端版本。
* 如果许可证服务器希望允许较旧的客户端忽略设备功能要求，请将支持的最低客户端版本设置为1(对于Adobe Access 2.0)。 服务器将向任何客户端版本2.0及更高版本颁发许可证。 如果客户端将许可证升级或转让给版本为2.0.2或更高版本的其他客户端，则将强制执行许可证中的设备功能要求，因为客户端现在将支持该使用规则。

