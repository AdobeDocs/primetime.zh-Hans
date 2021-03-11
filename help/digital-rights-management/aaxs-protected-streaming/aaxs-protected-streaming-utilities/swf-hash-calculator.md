---
title: SWF哈希计算器
description: SWF哈希计算器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# SWF哈希计算器{#swf-hash-calculator}

SWF哈希计算器实用程序计算文件中SWF应用程序的摘要。 要运行hasher，请运行命令：

```
Hasher.bat filename.swf
```

或命令：

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

实用程序将输出以下消息：

```
SWF Hash: hash-of-swf
```

此值可用于指定[!DNL flashaccess-tenant.xml]中的SWF摘要。
