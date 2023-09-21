---
description: SWF散列计算器实用程序计算位于文件中的SWF应用程序的摘要。
title: SWF哈希计算器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF哈希计算器{#swf-hash-calculator}

SWF散列计算器实用程序计算位于文件中的SWF应用程序的摘要。

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

您可以使用此值在中指定SWF摘要 [!DNL flashaccess-tenant.xml].
