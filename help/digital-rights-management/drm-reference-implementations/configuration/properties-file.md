---
title: 许可证服务器属性文件
description: 许可证服务器属性文件
copied-description: true
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 许可证服务器属性文件{#license-server-properties-file}

许可证服务器引用在中设置的属性 [!DNL flashaccess-refimpl.properties] 文件。 您可以直接引用该文件，以获取有关特定值的详细信息以及有关每个属性的使用信息。 功能齐全的示例请参见 [!DNL resources] 参考实施目录( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`)。

**凭据**  — 属性文件中包含Adobe发给您的凭据位置的设置。 您可以在以下位置指定这些凭据 [!DNL .pfx] 文件，或者为存储在HSM上的凭据提供别名和密码。 您至少需要配置与传输凭据和许可证服务器凭据相关的属性。 指定相对于您在 `config.resourcesDirectory` 属性。

**Flash媒体Rights Management服务器** - `flashaccess-refimpl.properties` 文件还包括多个与打包内容相关的属性。 这些属性仅用于Flash媒体Rights Management服务器1.x元数据转换。 修改此属性文件中的值后，要使更改生效，请重新启动许可证服务器。
