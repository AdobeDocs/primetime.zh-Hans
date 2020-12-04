---
description: Adobe建议，如果在配置文件中进行更改，则应在开始服务器之前运行配置验证程序实用程序。 此实用程序可以在请求处理过程中导致故障之前，及早检测大多数配置错误。
seo-description: Adobe建议，如果在配置文件中进行更改，则应在开始服务器之前运行配置验证程序实用程序。 此实用程序可以在请求处理过程中导致故障之前，及早检测大多数配置错误。
seo-title: 配置验证程序
title: 配置验证程序
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Configuration validator{#configuration-validator}

Adobe建议，如果在配置文件中进行更改，则应在开始服务器之前运行配置验证程序实用程序。 此实用程序可以在请求处理过程中导致故障之前，及早检测大多数配置错误。

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

对于每个许可证服务器配置文件，验证程序可以执行基于文件的验证，这确保XML文件格式良好，符合配置文件模式。

要对全局配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-global.xml --global
```

要对租户配置文件执行基于文件的验证，请键入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

Validator还可以执行基于部署的验证。 除了检查是否符合模式，此验证级别还验证您指定的值是否有效。 例如，它可确保引用的文件存在。

可在以下级别执行基于部署的验证：

* `Tenant` —验证特定租户的配置文件和凭据。如果要验证`<tenant1>`的配置，请键入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` —验证所有租户的全局配置文件和租户验证。如果要执行基于部署的全局验证，请键入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

