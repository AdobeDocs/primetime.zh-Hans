---
title: 撤消DRM客户端和运行时凭据
description: 撤消DRM客户端和运行时凭据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 撤消DRM客户端和运行时凭据{#revoking-drm-client-and-runtime-credentials}

DRM/运行时版本由安全级别、版本号和其他属性（包括操作系统和运行时）标识。 要限制允许的DRM/运行时版本，请在策略或 `HandlerConfiguration`. 模块限制可以包括最低安全级别和不允许颁发许可证的模块版本列表。 请参阅 [DRM客户端阻止列表受限制无法访问受保护的内容](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) 有关用于标识DRM/运行时模块的属性的详细信息。

如果设置了最低安全级别，则客户端上的版本（在计算机令牌中指定）必须大于或等于指定的值。

如果指定了排除版本的列表，并且客户端的版本与列表中的任何版本标识符匹配，则将不允许客户端使用包含此ModuleRequirements实例的权限。 为了使模块匹配版本信息，在版本信息中指定的所有参数（发行版本除外）必须与模块的值完全匹配。 如果客户端模块的值小于或等于版本信息中的值，则发行版本匹配。

如果报告特定DRM客户端或运行时版本发生违规，内容所有者和内容分发者（运行许可证服务器）可以配置服务器在Adobe没有可用的修补程序期间拒绝颁发许可证。 这可以通过以下方式配置 `HandlerConfiguration` 例，或透过更改所有政策而作出修订。 在后一种情况下，您可以维护策略更新列表，并使用它来检查策略是否已更新或撤销。

如果您需要较新版本的Adobe®Flash®播放器/Adobe® AIR®运行时或Adobe内容保护库（DRM模块），请更新策略，如中所示 [使用Java API更新策略](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) 并创建策略更新列表，或设置限制 `HandlerConfiguration` 通过调用 `HandlerConfiguration.setRuntimeModuleRequirements()` 或 `HandlerConfiguration.setDRMModuleRequirements()`. 当用户请求启用这些阻止列表的新许可证时，必须先安装较新的运行时间和库，然后才能颁发许可证。 有关列出DRM和运行时版本的块的示例，请参阅中的示例代码 [使用Java API更新策略](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
