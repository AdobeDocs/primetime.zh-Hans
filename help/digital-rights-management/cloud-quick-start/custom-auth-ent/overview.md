---
title: BEES概述
description: BEES概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# BEES概述{#bees-overview}

您可以实施后端授权服务(BEES)，为Primetime Cloud DRM操作提供自定义授权。

默认情况下，Primetime Cloud DRM使用匿名许可证交付。 这意味着发送到Primetime Cloud DRM的所有许可证请求都将返回有效的许可证，而不执行任何其他身份验证/授权检查(除非您应用了要求使用Adobe Primetime身份验证的策略限制)。

许可证请求包含在内容打包/加密期间使用的DRM策略。 DRM策略用于生成返回到客户端的DRM许可证。 在默认方案中，您必须在内容打包时做出所有DRM策略决策。 希望更好地控制这些工作流的客户具有以下选项：

1. 集成Primetime身份验证以在播放之前添加额外的权利检查。
1. 创建本地权利服务，Primetime Cloud DRM在允许任何设备播放您已打包的内容之前将查询该服务。

您的内部部署授权服务必须提供对Primetime Cloud DRM的响应，其中包括以下两个数据：

* `isAllowed`
* `drmPolicyToUse`

这些选项决定设备是否允许播放内容，以及使用哪个DRM策略来生成DRM许可证(如果 `isAllowed` 为真)。

本文档介绍实现上述选项2所需执行的操作：实施您自己的本地外部权利服务，并向Primetime Cloud DRM提供您已打包的内容。
