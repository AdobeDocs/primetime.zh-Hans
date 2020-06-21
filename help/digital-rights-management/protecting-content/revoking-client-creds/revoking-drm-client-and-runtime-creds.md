---
seo-title: 撤销DRM客户端和运行时凭据
title: 撤销DRM客户端和运行时凭据
uuid: 8e36536a-8eed-4d27-8a5f-8d3219817e57
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# 撤销DRM客户端和运行时凭据 {#revoking-drm-client-and-runtime-credentials}

DRM/运行时版本由安全级别、版本号和其他属性来标识，包括操作系统和运行时。 要限制允许的DRM/运行时版本，请在DRM策略中或在中设置模块限制 `HandlerConfiguration`。 模块限制可以包括不允许颁发许可证的模块版本的最低安全级别和列表。

有关 [用于标识DRM/运行时模块的属性的详细信息](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) ，请参阅限制访问受保护内容的DRM客户端的块列表。

如果设置了最低安全级别，则客户端上的版本（在计算机令牌中指定）必须大于或等于指定值。

如果指定了被排除版本的列表，且该客户端的版本与该列表中的任何版本标识符匹配，则不允许该客户端使用包含此ModuleRequirements实例的权利。 对于要匹配版本信息的模块，版本信息中指定的所有参数（发行版本除外）必须与模块的值完全匹配。 如果客户端模块的值小于或等于版本信息中的值，则发行版本匹配。

在报告特定DRM客户端或运行时版本的违规事件中，内容所有者和内容分发者（运行许可证服务器）可以配置服务器在Adobe没有可修复的期间拒绝颁发许可证。 可以按照上述说 `HandlerConfiguration` 明，或通过更改所有DRM策略来配置。 在后一种情况下，您可以维护DRM策略更新列表，并使用它检查DRM策略是否已更新或已吊销。

如果您需要Adobe Flash Player/Adobe AIR Runtime或Adobe内容保护库（DRM模块）的更新版本，您需要更新DRM策略。

请参 [阅使用Java API更新策略](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md)。

然后，您需要创建DRM策略更新列表，或通过调用或 `HandlerConfiguration` 设置 `HandlerConfiguration.setRuntimeModuleRequirements()` 限制 `HandlerConfiguration.setDRMModuleRequirements()`。 当用户请求启用了指定块列表的新许可证时，您需要安装最新的运行时和库，然后才能颁发许可证。

请参阅使用Java API [更新策略中的示例代码。有关列出DRM和运行时版本的块示例](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) ，请参阅列出DRM和运行时版本的块示例。
