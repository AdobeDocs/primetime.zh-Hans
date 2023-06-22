---
description: SWF哈希计算器实用程序计算位于文件中的SWF应用程序的摘要。
title: SWF哈希计算器
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF哈希计算器{#swf-hash-calculator}

SWF哈希计算器实用程序计算位于文件中的SWF应用程序的摘要。

要运行哈希程序，请键入：

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

该实用程序显示以下消息：

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

您可以使用此值来指定SWF摘要，位于 [!DNL flashaccess-tenant.xml].
