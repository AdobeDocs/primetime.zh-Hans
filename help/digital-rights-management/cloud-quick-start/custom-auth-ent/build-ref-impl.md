---
seo-title: 构建BEES参考实施
title: 构建BEES参考实施
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 构建BEES参考实现{#build-the-bees-reference-implementation}

确保您使用的是Java 1.6.0_24或更高版本。
1. 在[!DNL build-bees.xml]中填写所需的空路径，如`tomcatdir`和`fasterxmldir`

   包含FasterXML/Jackson。 您也可以从[https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core)下载它。
1. 如果要使用不同版本的Jackson库，请更新[!DNL build.common.xml]中的实际jar文件名。
1. 运行[!DNL build-bees.xml]的`all`目标:

   ```
   ant -f build-bees.xml
   ```

将在[!DNL bees-build/wars]文件夹中创建[!DNL bees.war]。