---
seo-title: 最低客户端版本
title: 最低客户端版本
uuid: f2b56cff-96fa-4954-a08a-9b3e78f496d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 最低客户端版本 {#minimum-client-version}

Adobe Primetime DRM 2.0.2及更高版本引入了一些Primetime DRM 2.0客户端不理解的新使用规则。 通过设置支持的最低客户端版本( `HandlerConfiguration.setMinSupportedClientVersion()`)，许可证服务器可以控制当旧客户端遇到具有这些使用规则的许可证时其行为方式。 根据此设置，服务器可以指示旧客户端是否可以忽略他们不了解的使用规则，或者旧客户端是否无法使用这些使用规则使用许可证。

例如，

* 如果许可证指定了设备功能要求(播放受保护内容需要 [设备功能](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md))，则Primetime DRM客户端2.0.2及更高版本可以执行这些要求。
* 如果许可证服务器不希望内容在不了解设备功能要求的客户端上播放，请将支持的最低客户端版本设置为2（对于2.0.2）。 这将阻止服务器在2.0.2之前向Primetime DRM客户端发放许可证。如果许可证从一个客户端传输到另一个客户端，则也会实施最低客户端版本。
* 如果许可证服务器希望允许较旧的客户端忽略设备功能要求，请将支持的最低客户端版本设置为1（对于Primetime DRM 2.0）。 然后，服务器向任何客户端版本2.0及更高版本发放许可证。 如果客户端将许可证升级或转让给版本为2.0.2或更高版本的其他客户端，则许可证中的设备功能要求随后会得到执行，因为客户端随后可以支持该使用规则。

