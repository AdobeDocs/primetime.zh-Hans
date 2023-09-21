---
title: 疑难解答
description: 疑难解答
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 疑难解答{#troubleshooting}

* 对于某些运行API级别10或更低级别的旧设备，由于权限问题，logcat无法打开日志设备。 将出现以下例外： `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **解决方法：**

   1. 打开 [!DNL AndroidManifest.xml] 在 [!DNL CatalogActivity] 项目。

   1. 将以下权限添加到 [!DNL `AndroidManfest.xml`] 文件：

      ```
      android.permission.READ_LOGS
      ```
