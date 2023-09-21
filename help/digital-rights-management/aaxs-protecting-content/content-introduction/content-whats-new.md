---
description: Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，可以创建策略，将策略应用到包含音频和视频内容的文件，并对这些文件进行加密。 执行这些任务的高层次步骤如下
title: 概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 概述 {#overview}

Adobe® Access™是用于高价值视听内容的高级数字版权管理和内容保护解决方案。 使用您使用Java API创建的工具，可以创建策略，将策略应用到包含音频和视频内容的文件，并对这些文件进行加密。 执行这些任务的高层次步骤如下：

1. 使用Java API设置策略属性和加密参数。
1. 创建描述内容的使用角色的策略。 (请参阅 [使用策略](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md))。

   您可以创建任意数量的策略。 大多数用户会创建少量策略并将其应用于许多文件。

1. 打包媒体文件。

   在这种情况下， *打包文件* 意味着加密它并对它应用策略。 (请参阅 [正在打包媒体文件](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. 实施许可证服务器以向用户颁发许可证。

加密内容现在已准备好进行部署，客户端可以从服务器请求许可证。

该SDK提供了一个Java API来完成这些任务，其中包括许可证服务器的参考实现以及基于Java API的命令行工具。 有关信息，请参阅 *使用Adobe访问引用实施*.

## Adobe访问5.2的新增功能 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **外部CEK**：能够将内容密钥管理系统(CKMS)集成到DRM许可证服务和内容打包工作流，而不是加密CEK并将其捆绑到内容的元数据中。 请参阅 [Adobe访问DRM外部CEK概述](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **许可证（优惠券）退货**：客户端返回（或删除）颁发给客户端的许可证的功能。
* **Xbox Key Server**：能够保护发送到Xbox和Xbox 360的内容。 (需要Adobe Primetime客户端。)

## 自定义使用规则 {#custom-usage-rules}

指定自定义使用规则。 自定义数据可包含在许可证服务器颁发的许可证中。 此数据的解释/处理完全取决于客户端应用程序和许可证服务器的实施。

示例用例：通过允许作为策略和/或内容许可证的一部分安全地传输其他业务规则，实现了使用规则的可扩展性。 出于安全原因，由于这些使用规则是在自定义客户端应用程序代码中强制实施的，因此此选项应与AIR应用程序或Flash PlayerSWF允许列表选项结合使用。 有关更多信息，请参阅 [运行时和应用程序限制](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
