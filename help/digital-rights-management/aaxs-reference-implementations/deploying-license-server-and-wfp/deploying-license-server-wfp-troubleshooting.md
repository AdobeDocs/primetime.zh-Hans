---
title: 疑难解答
description: 疑难解答
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 疑难解答 {#troubleshooting}

下面列出了用于部署的常见问题和解决方案：

* 如果您看到以下错误：

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   确保使用提供的对密码进行加密 `ScrambleUtil` 类。

* 如果您看到以下错误：

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   确保为PFX文件指定了正确的加密密码。

* 如果您看到以下错误：

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   确保您使用了Reference Implementation提供的password scrambler类(此scrambler实用程序与Adobe® Access™ Server for Protected Streaming提供的实用程序不同)。
