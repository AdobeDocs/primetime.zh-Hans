---
title: 配置验证程序
description: 配置验证程序
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# 配置验证程序{#configuration-validator}

Adobe建议在对配置文件进行任何更改之前，先运行Configuration Validator实用程序，然后再启动服务器。 此实用程序可以在请求处理过程中导致故障之前，及早检测大多数配置错误。

要运行验证程序，请使用命令：

```
Validator.bat options  
```

或命令：

```
java -jar libs/flashaccess-validator.jar options 
```

对于每个许可证服务器配置文件，验证程序可以执行基于文件的验证，这可确保XML文件格式良好，并符合配置文件模式。 要对全局配置文件执行基于文件的验证，请运行以下命令：

```
Validator --file path/flashaccess-global.xml --global
```

要对租户配置文件执行基于文件的验证，请运行以下命令：

```
Validator --file path/flashaccess-tenant.xml --tenant
```

验证程序还可以执行基于部署的验证；除了检查是否符合模式之外，此验证级别还检查指定的值是否有效（例如，它确保引用的文件存在）。 基于部署的验证可以在两个级别执行：

* 租户 — 验证特定租户的配置文件和凭据。 要验证“tenant1”的配置，请运行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 全局 — 验证所有租户的全局配置文件和租户验证。 要执行基于部署的全局验证，请运行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```

