---
title: Java系统属性
description: Java系统属性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Java系统属性{#java-system-properties}

可以选择设置以下两个Java系统属性以修改许可证服务器的配置和日志文件的位置：

* *LicenseServer.ConfigRoot*  — 包含许可证服务器的所有配置文件的目录。有关这些文件内容的详细信息，请参阅“[许可证服务器配置文件](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)”。 如果未设置，则默认值为&#x200B;*CATALINA_BASE/licenseserver*。
* *LicenseServer.LogRoot*  — 写入许可证服务器应用程序日志的“logs”文件夹的目录。如果未设置，则默认值为&#x200B;*LicenseServer.ConfigRoot*。

如果您使用[!DNL catalina.bat]或[!DNL catalina.sh]开始Tomcat，则可以使用`JAVA_OPTS`环境变量轻松设置这些系统属性。 启动Tomcat时，将使用此处设置的任何Java选项。 例如，设置：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

