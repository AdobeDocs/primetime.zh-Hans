---
title: 配置验证器
description: 配置验证器
copied-description: true
exl-id: 9b73e107-6ab7-4089-b415-0af8c9f86995
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 配置验证器 {#configuration-validator}

Adobe建议在启动服务器之前，在对配置文件进行任何更改之前运行配置验证器实用程序。 该实用程序可以及早检测大多数配置错误，以免这些错误在请求处理期间导致失败。

要运行验证器，请使用以下命令：

```
Validator.bat options  
```

或命令：

```
java -jar libs/flashaccess-validator.jar options 
```

对于每个许可证服务器配置文件，验证器可以执行基于文件的验证，从而确保XML文件格式正确，并且符合配置文件模式。 要对全局配置文件执行基于文件的验证，请运行以下命令：

```
Validator --file path/flashaccess-global.xml --global
```

要对租户配置文件执行基于文件的验证，请运行命令：

```
Validator --file path/flashaccess-tenant.xml --tenant
```

验证器还可以执行基于部署的验证；除了检查与架构的符合性之外，此级别的验证还会检查指定的值是否有效（例如，确保引用的文件存在）。 基于部署的验证可以在两个级别执行：

* 租户 — 验证特定租户的配置文件和凭据。 要验证“tenant1”的配置，请运行命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 全局 — 验证所有租户的全局配置文件和租户验证。 要执行基于部署的全局验证，请运行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
