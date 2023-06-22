---
title: SWF哈希计算器
description: SWF哈希计算器
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF哈希计算器{#swf-hash-calculator}

SWF哈希计算器实用程序计算位于文件中的SWF应用程序的摘要。 要运行哈希程序，请运行以下命令：

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
