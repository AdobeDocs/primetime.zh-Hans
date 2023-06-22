---
title: Java系统属性
description: Java系统属性
copied-description: true
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Java系统属性 {#java-system-properties}

可以选择设置以下两个Java系统属性来修改许可证服务器的配置和日志文件的位置：

* *LicenseServer.ConfigRoot*  — 包含许可证服务器的所有配置文件的目录。 有关这些文件内容的详细信息，请参阅&quot;[许可证服务器配置文件](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)“。 如果未设置，则默认为 *CATALINA_BASE/licenseserver*.
* *LicenseServer.LogRoot*  — 写入许可证服务器应用程序日志的“日志”文件夹的目录。 如果未设置，则默认为 *LicenseServer.ConfigRoot*.

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 要启动Tomcat，可以使用 `JAVA_OPTS` 环境变量。 此处设置的任何Java选项都将在启动Tomcat时使用。 例如，设置：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
