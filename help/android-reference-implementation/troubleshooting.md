---
seo-title: 疑难解答
title: 疑难解答
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# 疑难解答{#troubleshooting}

* 对于运行API级别10或更早版本的某些旧设备，由于权限问题，日志无法打开日志设备。 出现以下异常：`java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **解决方法：**

   1. 打开工作区中[!DNL CatalogActivity]项目下的[!DNL AndroidManifest.xml]。

   1. 为[!DNL `AndroidManfest.xml`]文件添加以下权限：

      ```
      android.permission.READ_LOGS
      ```
