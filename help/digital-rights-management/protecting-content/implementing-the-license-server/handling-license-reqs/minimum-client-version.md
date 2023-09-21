---
title: 最低客户端版本
description: 最低客户端版本
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 最低客户端版本 {#minimum-client-version}

Adobe Primetime DRM 2.0.2及更高版本引入了一些新的使用规则，Primetime DRM 2.0客户端不了解这些规则。 通过设置支持的最低客户端版本( `HandlerConfiguration.setMinSupportedClientVersion()`)，则许可证服务器可以控制旧客户端在遇到具有这些使用规则的许可证时的行为。 基于此设置，服务器可以指示较旧的客户端是否可以忽略它们不了解的使用规则，或者较旧的客户端是否将不能使用这些使用规则的许可证。

例如，

* 如果许可证指定设备功能要求( [播放受保护内容所需的设备功能](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md))，Primetime DRM客户端2.0.2及更高版本可以强制执行这些要求。
* 如果许可证服务器不希望内容在不了解设备功能要求的客户端上播放，请将支持的最低客户端版本设置为2（对于2.0.2）。 这将阻止服务器向2.0.2之前的Primetime DRM客户端颁发许可证。如果许可证从一个客户端传输到另一个客户端，则也会强制执行最低客户端版本。
* 如果许可证服务器希望允许较旧的客户端忽略设备功能要求，请将支持的最低客户端版本设置为1（对于Primetime DRM 2.0）。 然后，服务器向任何客户端版本2.0及更高版本颁发许可证。 如果客户端将许可证升级或传输到另一个版本2.0.2或更高版本的客户端，则强制实施许可证中的设备功能要求，因为客户端随后可以支持该使用规则。
