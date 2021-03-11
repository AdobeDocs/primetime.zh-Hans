---
title: 疑难解答
description: 疑难解答
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# 疑难解答{#troubleshooting}

* 对于运行API级别10或更低版本的某些旧设备，由于权限问题，日志无法打开日志设备。 出现以下异常：`java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **解决方法：**

   1. 打开工作区中[!DNL CatalogActivity]项目下的[!DNL AndroidManifest.xml]。

   1. 将以下权限添加到[!DNL `AndroidManfest.xml`]文件：

      ```
      android.permission.READ_LOGS
      ```
