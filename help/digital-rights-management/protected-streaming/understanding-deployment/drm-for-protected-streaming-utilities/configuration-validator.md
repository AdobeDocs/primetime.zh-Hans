---
description: Adobe建议，如果在配置文件中进行更改，应在启动服务器之前运行Configuration Validator实用程序。 该实用程序可以及早检测到大多数配置错误，以免这些错误在请求处理期间导致失败。
title: 配置验证器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 配置验证器{#configuration-validator}

Adobe建议，如果在配置文件中进行更改，应在启动服务器之前运行Configuration Validator实用程序。 该实用程序可以及早检测到大多数配置错误，以免这些错误在请求处理期间导致失败。

要运行验证器，请键入：

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

对于每个许可证服务器配置文件，验证器可以执行基于文件的验证，从而确保XML文件格式正确并且符合配置文件模式。

要对全局配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-global.xml --global
```

要对租户配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

验证器还可以执行基于部署的验证。 除了检查是否符合架构，此级别的验证还会验证您指定的值是否有效。 例如，它可确保引用的文件存在。

可以在以下级别执行基于部署的验证：

* `Tenant`  — 验证特定租户的配置文件和凭据。 如果要验证配置， `<tenant1>`，类型：

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
  ```

* `Global`  — 验证所有租户的全局配置文件和租户验证。 如果要执行基于部署的全局验证，请键入：

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -g
  ```
