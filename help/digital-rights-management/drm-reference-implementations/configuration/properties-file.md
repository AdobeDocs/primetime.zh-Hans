---
title: 许可证服务器属性文件
description: 许可证服务器属性文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 许可证服务器属性文件{#license-server-properties-file}

许可证服务器引用在[!DNL flashaccess-refimpl.properties]文件中设置的属性。 您可以直接引用该文件，了解有关特定值的详细信息以及有关每个属性的使用信息。 在参考实现的[!DNL resources]目录(`([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`)中提供了全功能示例。

**凭据**  — 属性文件包含Adobe向您发出的凭据位置设置。您可以在[!DNL .pfx]文件中指定这些凭据，并使用口令，或为存储在HSM上的凭据提供别名和口令。 您至少需要配置与传输凭据和许可证服务器凭据相关的属性。 指定凭据文件相对于您在`config.resourcesDirectory`属性中指定的目录的位置。

**Flash Media Rights Management Server**  — 文 `flashaccess-refimpl.properties` 件还包括若干与打包内容相关的属性。这些属性仅用于Flash Media Rights Management Server 1.x元数据转换。 修改此属性文件中的值后，如果更改生效，请重新启动许可证服务器。
