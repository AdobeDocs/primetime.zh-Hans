---
title: 密码加扰器
description: 密码加扰器
copied-description: true
exl-id: ceedd61e-918b-453f-8d21-628b2d8713ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 密码加扰器 {#password-scrambler}

Password Scrambler实用程序对密码进行加密，以便在Adobe Access Server for Protected Streaming配置文件中使用密码。 要运行扰频器，请运行以下命令：

```
Scrambler.bat password 
```

或命令：

```
java -jar libs/flashaccess-scrambler.jar password  
```

该实用程序输出以下消息：

```
Encrypted password: scrambled-password 
```

flashaccess-global.xml和flashaccess-tenant.xml中指定的所有口令都必须加密。

>[!NOTE]
>
>用于受保护流的Adobe Access Server中的Password Scrambler实用程序不能与Reference Implementation License Server随附的扰码器互换。
