---
description: 'null'
seo-description: 'null'
seo-title: 疑难解答
title: 疑难解答
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
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

   确保在PFX文件中指定了正确的加密密码。

* 如果显示以下错误消息：

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   确保使用随Reference Implementation *提供的密码扰码器类*。 此扰码器实用程序与随Adobe PrimetimeDRM服务器提供的用于受保护流的实用程序不同。

