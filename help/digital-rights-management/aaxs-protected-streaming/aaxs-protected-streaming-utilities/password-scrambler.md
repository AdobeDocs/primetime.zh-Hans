---
title: 密码剪贴器
description: 密码剪贴器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 密码剪贴器{#password-scrambler}

密码剪贴器实用程序加密密码，以便在Adobe Access Server中对受保护流配置文件使用。 要运行scrambler，请运行命令：

```
Scrambler.bat password 
```

或命令：

```
java -jar libs/flashaccess-scrambler.jar password  
```

实用程序输出以下消息：

```
Encrypted password: scrambled-password 
```

在flashaccess-global.xml和flashaccess-tenant.xml中指定的所有口令都必须加密。

>[!NOTE]
>
>Adobe Access Server中用于受保护流的密码扰码器实用程序不能与随参考实施许可证服务器提供的扰码器互换。

