---
seo-title: 蜜蜂概述
title: 蜜蜂概述
uuid: c6ee7528-fdfa-4a56-bea2-a5e2dab6d428
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 蜜蜂概述{#bees-overview}

您可以实施后端授权服务(BEES)，为您的Primetime Cloud DRM操作提供自定义授权。

默认情况下，Primetime Cloud DRM使用匿名许可证交付。 这意味着发送到Primetime Cloud DRM的所有许可证请求将返回有效的许可证，而无需执行任何其他身份验证／授权检查（除非您已应用了需要使用Adobe Primetime身份验证的策略限制）。

许可证请求包含在内容打包／加密过程中使用的DRM策略。 DRM策略用于生成返回给客户端的DRM许可证。 在默认情况下，您必须在内容打包时做出所有DRM策略决策。 希望对这些工作流进行更精细控制的客户有以下选项：

1. 集成Primetime身份验证，在播放前添加额外的授权检查。
1. 创建Primetime Cloud DRM将在允许任何设备播放您打包的内容之前查询的内部授权服务。

您的内部授权服务必须对包含以下两段数据的Primetime Cloud DRM提供响应：

* `isAllowed`
* `drmPolicyToUse`

这些选项确定是否允许设备播放内容，以及使用哪个DRM策略生成DRM许可证(如果 `isAllowed` 为true)。

本文档涵盖完成上述选项2所需完成的工作：实施您自己的内部外部授权服务，并将其发布到Primetime Cloud DRM，获取您打包的内容。
