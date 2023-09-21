---
title: SWF哈希计算器
description: SWF哈希计算器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF哈希计算器{#swf-hash-calculator}

SWF哈希计算器实用程序计算了一个位于文件中的SWF应用程序的摘要。 要运行哈希程序，请运行以下命令：

```
Hasher.bat filename.swf
```

或命令：

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

该实用程序输出以下消息：

```
SWF Hash: hash-of-swf
```

此值可用于指定中的SWF摘要 [!DNL flashaccess-tenant.xml].
