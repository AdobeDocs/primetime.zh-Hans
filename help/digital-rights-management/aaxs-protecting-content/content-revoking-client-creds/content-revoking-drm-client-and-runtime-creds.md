---
seo-title: 撤销DRM客户端和运行时凭据
title: 撤销DRM客户端和运行时凭据
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 撤销DRM客户端和运行时凭据{#revoking-drm-client-and-runtime-credentials}

DRM/运行时版本由安全级别、版本号和其他属性（包括操作系统和运行时）标识。 要限制允许的DRM/运行时版本，请在策略中或在中设置模块限制 `HandlerConfiguration`。 模块限制可以包括最低安全级别和不允许颁发许可证的模块版本列表。 有关 [用于标识DRM/运行时模块的属性的详细信息](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blacklist-drm-clients.md) ，请参阅DRM客户端限制访问受保护内容的黑名单。

如果设置了最低安全级别，则客户端上的版本（在计算机令牌中指定）必须大于或等于指定值。

如果指定了被排除版本列表，并且客户端的版本与列表中的任何版本标识符匹配，则客户端将不允许使用包含此ModuleRequirements实例的权限。 对于要匹配版本信息的模块，版本信息中指定的所有参数（发行版除外）必须与模块的值完全匹配。 如果客户端模块的值小于或等于版本信息中的值，则发行版本匹配。

如果向特定DRM客户端或运行时版本报告了违反情况，内容所有者和内容分发者（运行许可证服务器）可以配置服务器在Adobe没有可用修复的期间拒绝发行许可证。 这可以通过上述 `HandlerConfiguration` 配置，或通过更改所有策略进行配置。 在后一种情况下，您可以维护策略更新列表，并使用它检查策略是否已更新或已撤销。

如果需要Adobe® Flash® Player/Adobe® AIR® Runtime或Adobe内容保护库（DRM模块）的更新版本，请使用Java API更新策略和创建策略更新列表中所示的策略，或在中通过调用或 [设置限](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) 制 `HandlerConfiguration``HandlerConfiguration.setRuntimeModuleRequirements()``HandlerConfiguration.setDRMModuleRequirements()`。 当用户在启用这些黑名单的情况下请求新的许可证时，必须安装较新的运行时和库，才能颁发许可证。 有关黑名单DRM和运行时版本的示例，请参阅使用Java API [更新策略中的示例代码](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)。
