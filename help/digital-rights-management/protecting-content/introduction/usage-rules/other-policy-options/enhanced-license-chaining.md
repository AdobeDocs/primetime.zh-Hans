---
title: 增强的许可证链接
description: 增强的许可证链接
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 增强的许可证链{#enhanced-license-chaining}

您可以使用增强的许可证链接通过使用父根许可证批量更新许可证来更新许可证。

Primetime DRM 2.0支持许可证链，其中叶和根许可证都绑定到特定计算机。 Primetime DRM 3.0及更高版本支持增强的许可证链接，其中叶绑定到根许可证，而只有根许可证绑定到特定计算机或域。 增强的许可证链接支持将叶许可证嵌入到内容中，并且客户端只需从许可证服务器获取根许可证即可使用受保护的内容。

如果要启用增强的许可证链接，则必须为Primetime DRM策略分配根加密密钥。 根加密密钥用于将叶许可证加密绑定到根许可证。

>[!NOTE]
>
>Primetime DRM客户端版本3.0或更高版本支持增强的许可证链接。 如果较旧的客户端请求支持增强许可证链接的内容的许可证，则许可证服务器仍可通过使用Primetime DRM 2.0支持的许可证链接向此客户端颁发许可证。

示例用例：通过下载单个根许可证，使用此选项更新任何链接的许可证。 例如，实施订阅模型，只要用户每月重新发布订阅，就可以回放内容。 这种方法的好处是用户只需获得单个许可证即可更新其所有订阅许可证。
