---
title: 撤销DRM客户端和运行时凭据
description: 撤销DRM客户端和运行时凭据
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# 撤销DRM客户端和运行时凭据{#revoking-drm-client-and-runtime-credentials}

DRM/运行时版本由安全级别、版本号和其他属性（包括操作系统和运行时）来标识。 要限制允许的DRM/运行时版本，请在策略或`HandlerConfiguration`中设置模块限制。 模块限制可包括不允许颁发许可证的模块版本的最低安全级别和列表。 有关用于标识DRM/运行时模块的属性的详细信息，请参阅[ DRM客户端阻止列表（限制访问受保护内容）](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md)。

如果设置了最低安全级别，则客户端上的版本（在计算机令牌中指定）必须大于或等于指定值。

如果指定了排除版本的列表，且客户端的版本与列表中的任何版本标识符匹配，则客户端将不允许使用包含此ModuleRequirements实例的权限。 对于要匹配版本信息的模块，版本信息中指定的所有参数（发行版除外）必须完全匹配模块的值。 如果客户端模块的值小于或等于版本信息中的值，则发行版本匹配。

在事件中，用特定DRM客户端或运行时版本报告违规，内容所有者和内容分发者（运行许可证服务器）可以配置服务器在Adobe没有可用修复的期间拒绝颁发许可证。 可以通过上面所述的`HandlerConfiguration`进行配置，也可以通过更改所有策略进行配置。 在后一种情况下，您可以维护策略更新列表，并使用它检查策略是否已更新或吊销。

如果需要较新版本的Adobe® Flash® Player/Adobe® AIR® Runtime或Adobe内容保护库（DRM模块），请按照[使用Java API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)更新策略中的说明更新策略并创建策略更新列表，或通过调用`HandlerConfiguration.setRuntimeModuleRequirements()`或`HandlerConfiguration.setDRMModuleRequirements()`在`HandlerConfiguration`中设置限制。 当用户请求启用这些阻止列表的新许可证时，必须先安装较新的运行时和库，然后才能颁发许可证。 有关列出DRM和运行时版本的块的示例，请参阅[使用Java API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)更新策略中的示例代码。
