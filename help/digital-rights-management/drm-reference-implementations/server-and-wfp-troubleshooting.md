---
title: 疑难解答
description: 疑难解答
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 疑难解答{#troubleshooting}

以下是在部署过程中可能遇到的一些问题和解决方案。

* 如果显示以下错误消息：

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   确保已使用`ScrambleUtil`类加密密码。

* 如果显示以下错误消息：

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   请确保在PFX文件中指定了正确的加密密码。

* 如果显示以下错误消息：

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   请确保使用随Reference Implementation *提供的口令scrambler类*。 此扰码器实用程序与随Adobe Primetime DRM Server提供的用于受保护流的实用程序不同。

