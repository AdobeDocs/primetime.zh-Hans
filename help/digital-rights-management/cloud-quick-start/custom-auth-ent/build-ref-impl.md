---
title: 构建BEES参考实施
description: 构建BEES参考实施
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 构建BEES参考实施 {#build-the-bees-reference-implementation}

确保您使用的是Java 1.6.0_24或更高版本。
1. 填写所需的空路径，如 `tomcatdir` 和 `fasterxmldir` 在 [!DNL build-bees.xml]

   包括FailterXML/Jackson。 您也可以从以下位置下载： [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. 在中更新实际的jar文件名 [!DNL build.common.xml] 如果要使用其他版本的Jackson库，请执行以下操作。
1. 运行 `all` 目标 [!DNL build-bees.xml]：

   ```
   ant -f build-bees.xml
   ```

此 [!DNL bees.war] 将在以下创建： [!DNL bees-build/wars] 文件夹。
