---
seo-title: 生成本地DRM元数据
title: 生成本地DRM元数据
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 生成本地DRM元数据{#generate-the-on-premises-drm-metadata}

文件夹 [!DNL CreateMetadata.jar] 中包含一个实用程 [!DNL create_metadata] 序。 该实用程序的要点是创建一个本地DRM元数据，该元数据将启动客户端针对指定的本地个性化服务器执行个性化进程。

1. 使用以下文件更新Primetime DRM参考实施——命令行工具：

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      两个JAR文件可以驻留在文件夹 [!DNL Command Line Tools/libs] 中。 文 [!DNL createMetadata.properties] 件可以驻留在文件 [!DNL flashaccesstools.properties] 旁边。

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

包含一个 [!DNL examplecreate.sh] 脚本，用于演示元数据的示例创建。 在尝试生成元数据之前，请务必在脚本和属性文件中配置许可证服务器URL和个性化服务器URL。

公用事业的输入如下：

* `createMetadata.properties` -包含默认策略、证书位置和密码等的属性文件。
* `indivCert` -包含个性化传输证书的PKCS12文件
* `indivURL` -本地个性化服务器的URL

输出文件是DRM客户端将使用的本地DRM元数据文件。 例如：

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.