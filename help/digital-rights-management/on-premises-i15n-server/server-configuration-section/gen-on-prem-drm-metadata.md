---
title: 生成本地DRM元数据
description: 生成本地DRM元数据
copied-description: true
exl-id: b42e3491-081b-45bf-bd00-8fb769a97446
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 生成本地DRM元数据{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] 实用程序包含在 [!DNL create_metadata] 文件夹。 此实用工具的目的是创建本地DRM元数据，该元数据将启动客户端对指定的本地个性化服务器执行个性化流程。

1. 使用以下文件更新Primetime DRM参考实施 — 命令行工具：

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      两个JAR文件可以驻留在 [!DNL Command Line Tools/libs] 文件夹。 此 [!DNL createMetadata.properties] 文件可以驻留在旁边 [!DNL flashaccesstools.properties] 文件。

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

包含一个 [!DNL examplecreate.sh] 用于演示元数据的示例创建的脚本。 在尝试生成元数据之前，请确保在脚本和属性文件中配置许可证服务器URL和个性化服务器URL。

该公用程式的输入值如下：

* `createMetadata.properties`  — 包含默认策略、证书位置和密码等的属性文件。
* `indivCert`  — 包含个性化传输证书的PKCS12文件
* `indivURL`  — 内部部署个性化服务器的URL

输出文件是DRM客户端使用的本地DRM元数据文件。 例如：

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
