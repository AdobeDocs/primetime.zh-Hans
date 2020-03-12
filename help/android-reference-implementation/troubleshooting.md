---
seo-title: 疑难解答
title: 疑难解答
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 疑难解答{#troubleshooting}

* 对于运行API级别10或更低版本的某些旧设备，Logcat因权限问题而无法打开日志设备。 出现以下异常：解 `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` 决方 **法：**

   1. 在工 [!DNL AndroidManifest.xml] 作区中 [!DNL CatalogActivity] 的项目下打开。

   1. 向文件添加以下权 [!DNL `AndroidManfest.xml`] 限：

      ```
      android.permission.READ_LOGS
      ```
