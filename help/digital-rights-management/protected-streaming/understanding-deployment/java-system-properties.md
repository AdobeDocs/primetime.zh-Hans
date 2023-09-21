---
description: 您可以在许可证服务器上配置多个Java系统属性，以控制配置和日志文件的位置。
title: Java系统属性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Java系统属性{#java-system-properties}

您可以在许可证服务器上配置多个Java系统属性，以控制配置和日志文件的位置。

您可以选择配置以下Java系统属性：

* *`LicenseServer.ConfigRoot`*  — 包含许可证服务器配置文件的目录的名称。

  请参阅 *许可证服务器配置文件* 以了解有关这些文件内容的详细信息。 如果未配置，默认值为 `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot*  — 的名称 [!DNL logs] 许可证服务器应用程序日志所在的目录。 如果尚未修改此目录的名称，则将此目录名称配置为 *LicenseServer.ConfigRoot* 默认情况下。

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 文件启动Tomcat时，可以使用 `JAVA_OPTS` 环境变量。 在Tomcat启动时，将自动应用您配置的任何Java选项。

例如，您可以配置 `JAVA_OPTS` 环境变量，如下所示：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
