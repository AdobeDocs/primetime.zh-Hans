---
description: 'null'
seo-description: 'null'
seo-title: 许可证服务器属性文件
title: 许可证服务器属性文件
uuid: 5e94ed1f-1dbf-4506-a097-183fcd5d25ef
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证服务器属性文件{#license-server-properties-file}

许可证服务器引用文件中设置的 [!DNL flashaccess-refimpl.properties] 属性。 您可以直接引用该文件，以了解有关特定值的详细信息以及每个属性的使用信息。 在参考实现()的目 [!DNL resources] 录中提供了全功能的示 `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`例。

**凭据** -属性文件包含Adobe向您发出的凭据的位置设置。 您可以在文件中指定这些凭 [!DNL .pfx] 据，并使用口令，或者为存储在HSM上的凭证提供别名和口令。 您至少需要配置与传输凭证和许可证服务器凭证相关的属性。 指定凭证文件相对于您在属性中指定的目录的相对位 `config.resourcesDirectory` 置。

**Flash Media Rights Management Server** —— 该文 `flashaccess-refimpl.properties` 件还包括若干与打包内容相关的属性。 这些属性仅用于Flash Media Rights Management Server 1.x元数据转换。 修改此属性文件中的值后，如果更改生效，请重新启动许可证服务器。
