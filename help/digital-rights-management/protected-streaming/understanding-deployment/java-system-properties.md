---
description: 您可以在许可证服务器上配置多个Java系统属性，以控制配置和日志文件的位置。
title: Java系统属性
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Java系统属性{#java-system-properties}

您可以在许可证服务器上配置多个Java系统属性，以控制配置和日志文件的位置。

您可以选择配置以下Java系统属性：

* *`LicenseServer.ConfigRoot`*  — 包含许可证服务器的配置文件的目录的名称。

   参见 *许可证服务器配置文件* 以了解有关这些文件内容的详细信息。 如果未配置，默认值为 `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot*  — 的名称 [!DNL logs] 许可证服务器应用程序日志所在的目录。 如果尚未修改此目录的名称，则此目录名称将配置为 *LicenseServer.ConfigRoot* 默认情况下。

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 文件启动Tomcat时，可以使用 `JAVA_OPTS` 环境变量。 Tomcat启动时，将自动应用您配置的任何Java选项。

例如，您可以配置 `JAVA_OPTS` 环境变量，如下所示：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
