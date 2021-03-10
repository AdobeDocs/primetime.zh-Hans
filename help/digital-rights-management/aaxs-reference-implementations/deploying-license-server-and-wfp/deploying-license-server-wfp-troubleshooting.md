---
title: 疑难解答
description: 疑难解答
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# {#troubleshooting}疑难解答

以下列出了部署的常见问题和解决方案：

* 如果您看到以下错误：

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   确保使用提供的`ScrambleUtil`类加密密码。

* 如果您看到以下错误：

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   确保为PFX文件指定了正确的加密密码。

* 如果您看到以下错误：

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   确保您使用了随“参考实施”提供的口令scrambler类(此scrambler实用程序与随“Adobe® Access™ Server for Protected Streaming”提供的该实用程序不同)。

