---
description: Adobe建议，如果您在配置文件中进行更改，则应在启动服务器之前运行Configuration Validator实用程序。 此实用程序可以在请求处理过程中导致故障之前及早检测大多数配置错误。
seo-description: Adobe建议，如果您在配置文件中进行更改，则应在启动服务器之前运行Configuration Validator实用程序。 此实用程序可以在请求处理过程中导致故障之前及早检测大多数配置错误。
seo-title: 配置验证程序
title: 配置验证程序
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 配置验证程序{#configuration-validator}

Adobe建议，如果您在配置文件中进行更改，则应在启动服务器之前运行Configuration Validator实用程序。 此实用程序可以在请求处理过程中导致故障之前及早检测大多数配置错误。

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

对于每个许可证服务器配置文件，验证程序可以执行基于文件的验证，这可确保XML文件的格式良好并符合配置文件模式。

要对全局配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-global.xml --global
```

要对租户配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

Validator还可以执行基于部署的验证。 除了检查是否符合方案之外，此验证级别还验证您指定的值是否有效。 例如，它可确保引用的文件存在。

基于部署的验证可以在以下级别执行：

* `Tenant` — 验证特定租户的配置文件和凭据。 如果要验证配置，请键 `<tenant1>`入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — 验证所有租户的全局配置文件和租户验证。 如果要执行基于全局部署的验证，请键入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

