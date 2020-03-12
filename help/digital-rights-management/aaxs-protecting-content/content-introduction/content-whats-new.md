---
description: 'Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，您可以创建策略，将策略应用于包含音频和视频内容的文件，并加密这些文件。 执行这些任务的高级步骤如下 '
seo-description: 'Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，您可以创建策略，将策略应用于包含音频和视频内容的文件，并加密这些文件。 执行这些任务的高级步骤如下 '
seo-title: 概述
title: 概述
uuid: 874c175b-8207-49fa-aad4-204ccbee9c2c
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# 概述 {#overview}

Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，您可以创建策略，将策略应用于包含音频和视频内容的文件，并加密这些文件。 执行这些任务的高级步骤如下：

1. 使用Java API设置策略属性和加密参数。
1. 创建描述内容使用角色的策略。 (请参阅 [使用策略](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md))。

   您可以创建任意数量的策略。 大多数用户创建少量策略并将其应用于多个文件。

1. 打包媒体文件。

   在此上下文中， *打包文件意味着* ，对文件进行加密并对其应用策略。 (请参阅 [打包媒体文件](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)。)

1. 实施许可证服务器以向用户发放许可证。

加密内容现已准备好部署，客户端可以从服务器请求许可证。

SDK提供了用于完成这些任务的Java API，包括许可证服务器的参考实现以及基于Java API的命令行工具。 有关信息，请参 *阅使用Adobe Access Reference Implementations*。

## Adobe Access 5.2的新增功能 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **外部CEK**:将内容密钥管理系统(CKMS)集成到DRM许可证服务和内容打包工作流程的能力，而不是对CEK进行加密并将其捆绑到内容的元数据中。 请参 [阅Adobe Access DRM外部CEK概述](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)。

* **许可证（凭证）退回**:客户端可以返回（或删除）发给客户端的许可证。
* **Xbox Key Server**:保护发送到Xbox和Xbox 360的内容的能力。 （需要Adobe Primetime客户端。）

## 自定义使用规则 {#custom-usage-rules}

指定自定义使用规则。 自定义数据可以包含在由许可服务器颁发的许可中。 对这些数据的解释／处理完全取决于客户端应用程序和许可证服务器的实施。

示例用例：通过允许将其他业务规则作为策略和／或内容许可的一部分安全地传达，实现使用规则的可扩展性。 出于安全原因，因为这些使用规则是在自定义客户端应用程序代码中实施的，所以应将此选项与AIR应用程序或Flash Player SWF白名单选项结合使用。 有关详细信息，请参阅“运[行时和应用程序限制](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-whitelist-air.md)”。