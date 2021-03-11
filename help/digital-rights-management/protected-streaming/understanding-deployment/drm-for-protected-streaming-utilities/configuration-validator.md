---
description: Adobe建议，如果在配置文件中进行更改，则在开始服务器之前应运行Configuration Validator实用程序。 此实用程序可以在请求处理过程中导致故障之前，及早检测大多数配置错误。
title: 配置验证程序
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Configuration validator{#configuration-validator}

Adobe建议，如果在配置文件中进行更改，则在开始服务器之前应运行Configuration Validator实用程序。 此实用程序可以在请求处理过程中导致故障之前，及早检测大多数配置错误。

要运行验证程序，请键入：

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

对于每个许可证服务器配置文件，验证程序可以执行基于文件的验证，这可确保XML文件格式良好，并符合配置文件模式。

要对全局配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-global.xml --global
```

要对租户配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

验证程序还可以执行基于部署的验证。 除了检查是否符合模式之外，此验证级别还验证您指定的值是否有效。 例如，它可确保引用的文件存在。

可在以下级别执行基于部署的验证：

* `Tenant`  — 验证特定租户的配置文件和凭据。如果要验证`<tenant1>`的配置，请键入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global`  — 验证所有租户的全局配置文件和租户验证。如果要执行基于部署的全局验证，请键入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

