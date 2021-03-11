---
description: 'Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，您可以创建策略，将策略应用于包含音频和视频内容的文件，并加密这些文件。 执行这些任务的高级步骤如下 '
title: 概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# 概述{#overview}

Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，您可以创建策略，将策略应用于包含音频和视频内容的文件，并加密这些文件。 执行这些任务的高级步骤如下：

1. 使用Java API设置策略属性和加密参数。
1. 创建描述内容使用角色的策略。 （请参阅[使用策略](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)）。

   您可以创建任意数量的策略。 大多数用户会创建少量策略并将其应用于多个文件。

1. 打包媒体文件。

   在此上下文中，*打包文件*&#x200B;意味着对文件进行加密并对其应用策略。 （请参阅[打包媒体文件](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)。）

1. 实施许可证服务器以向用户颁发许可证。

加密内容现在已准备好部署，客户端可以从服务器请求许可证。

SDK提供用于完成这些任务的Java API，包括许可证服务器的参考实现以及基于Java API的命令行工具。 有关信息，请参阅&#x200B;*使用Adobe访问参考实现*。

## Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}的新增功能

* **外部CEK**:将内容密钥管理系统(CKMS)集成到DRM许可证服务和内容打包工作流的能力，而不是加密CEK并将其捆绑到内容的元数据中。请参阅[Adobe访问DRM外部CEK概述](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)。

* **许可证（凭证）退回**:客户端可以返回（或删除）颁发给客户端的许可证。
* **Xbox Key服务器**:保护发送到Xbox和Xbox 360的内容的能力。(需要Adobe Primetime客户端。)

## 自定义使用规则{#custom-usage-rules}

指定自定义使用规则。 自定义数据可以包含在由许可服务器颁发的许可中。 对这些数据的解释/处理完全取决于客户端应用程序和许可证服务器的实现。

示例用例：通过允许将其他业务规则作为策略和/或内容许可证的一部分安全地传达，实现使用规则的可扩展性。 出于安全原因，由于这些使用规则是在自定义客户端应用程序代码中强制实施的，因此应将此选项与AIR应用程序或Flash Player SWF允许列表选项结合使用。 有关详细信息，请参阅[运行时和应用程序限制](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md)。
