---
title: 撤消DRM客户端和运行时凭据
description: 撤消DRM客户端和运行时凭据
copied-description: true
exl-id: 3a91a256-ab01-48d8-99f3-854195faae6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 撤消DRM客户端和运行时凭据 {#revoking-drm-client-and-runtime-credentials}

DRM/运行时版本由安全级别、版本号和其他属性（包括操作系统和运行时）标识。 要限制允许的DRM/运行时版本，请在DRM策略或 `HandlerConfiguration`. 模块限制可以包括最低安全级别和不允许颁发许可证的模块版本列表。

参见 [DRM客户端访问受保护内容时受限制的阻止列表](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) 有关用于标识DRM/运行时模块的属性的详细信息。

如果设置了最低安全级别，则客户端上的版本（在计算机令牌中指定）必须大于或等于指定的值。

如果指定了排除版本的列表，并且客户端的版本与列表中的任何版本标识符匹配，则将不允许客户端使用包含此ModuleRequirements实例的权限。 要使模块匹配版本信息，在版本信息中指定的所有参数（发行版本除外）必须与模块的值完全匹配。 如果客户端模块的值小于或等于版本信息中的值，则发行版本匹配。

如果报告特定DRM客户端或运行时版本发生违规，内容所有者和内容分发者（运行许可证服务器）可以配置服务器在Adobe没有可用的修补程序期间拒绝颁发许可证。 这可以通过以下方式配置 `HandlerConfiguration` 如上所述，或通过更改所有DRM策略来执行。 在后一种情况下，您可以维护DRM策略更新列表，并使用它来检查DRM策略是否已更新或撤消。

如果您需要较新版本的AdobeFlash Player/Adobe AIR运行时或Adobe内容保护库（DRM模块），则需要更新DRM策略。

参见 [使用Java API更新策略](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

然后，您需要创建DRM策略更新列表或设置限制 `HandlerConfiguration` 通过调用 `HandlerConfiguration.setRuntimeModuleRequirements()` 或 `HandlerConfiguration.setDRMModuleRequirements()`. 当用户请求启用了指定阻止列表的新许可证时，您需要安装最新的运行时和库，然后才能颁发许可证。

请参阅中的示例代码 [使用Java API更新策略例如，有关列出DRM和运行时版本的块的示例](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) 有关列出DRM和运行时版本的块的示例。
