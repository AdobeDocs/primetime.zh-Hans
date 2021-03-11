---
description: 您可以在许可证服务器上配置多个Java系统属性，以控制配置和日志文件的位置。
title: Java系统属性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Java系统属性{#java-system-properties}

您可以在许可证服务器上配置多个Java系统属性，以控制配置和日志文件的位置。

您可以选择配置以下Java系统属性：

* *`LicenseServer.ConfigRoot`*  — 包含许可证服务器配置文件的目录的名称。

   有关这些文件内容的详细信息，请参阅&#x200B;*许可证服务器配置文件*。 如果未配置，则默认值为`CATALINA_BASE/licenseserver`。

* *LicenseServer.LogRoot*  — 许可证服 [!DNL logs] 务器应用程序日志所在目录的名称。如果尚未修改此目录的名称，则默认情况下，此目录的名称配置为&#x200B;*LicenseServer.ConfigRoot*。

如果使用[!DNL catalina.bat]或[!DNL catalina.sh]文件开始Tomcat，则可以使用`JAVA_OPTS`环境变量配置System属性。 在Tomcat开始时，您配置的任何Java选项都将自动应用。

例如，可以按如下方式配置`JAVA_OPTS`环境变量：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

