---
title: 疑难解答
description: 疑难解答
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 疑难解答{#troubleshooting}

* 对于某些运行API级别10或更低级别的旧设备， logcat无法打开日志设备，因为存在权限问题。 出现以下异常： `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **解决方法：**

   1. 打开 [!DNL AndroidManifest.xml] 在 [!DNL CatalogActivity] 项目。

   1. 将以下权限添加到 [!DNL `AndroidManfest.xml`] 文件：

      ```
      android.permission.READ_LOGS
      ```
