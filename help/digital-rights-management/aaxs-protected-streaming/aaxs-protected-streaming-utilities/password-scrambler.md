---
seo-title: 密码剪贴器
title: 密码剪贴器
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# 密码剪贴器 {#password-scrambler}

密码剪贴器实用程序加密密码，以便在Adobe Access Server中用于受保护的流配置文件。 要运行scrambler，请运行命令：

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
>Adobe Access Server中用于受保护流的密码扰码器实用程序不能与随参考实施许可服务器提供的扰码器互换。

