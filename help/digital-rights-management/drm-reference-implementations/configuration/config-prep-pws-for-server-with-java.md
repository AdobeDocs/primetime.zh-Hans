---
title: 使用Java准备口令
description: 使用Java准备口令
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---


# 使用Java{#prepare-passwords-using-java}准备口令

使用Java运行`ScrambleUtil.class`:

1. 导航到`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. 在命令行中，键入：

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

