---
seo-title: 构建BEES参考实现
title: 构建BEES参考实现
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 构建BEES参考实现 {#build-the-bees-reference-implementation}

确保您使用的是Java 1.6.0_24或更高版本。
1. 填充所需的空路径，如 `tomcatdir` 和 `fasterxmldir` 中 [!DNL build-bees.xml]

   包含FasterXML/Jackson。 您也可以从https://jar-download.com/artifacts/com.fasterxml.jackson.core下载 [它](https://jar-download.com/artifacts/com.fasterxml.jackson.core)。
1. 如果要使用其 [!DNL build.common.xml] 他版本的Jackson库，请在中更新实际的jar文件名。
1. 运行以 `all` 下目标 [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

将 [!DNL bees.war] 在文件夹中创 [!DNL bees-build/wars] 建。