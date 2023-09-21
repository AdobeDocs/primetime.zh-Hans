---
title: 疑难解答
description: 疑难解答
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 疑难解答{#troubleshooting}

以下是您在部署期间可能会遇到的一些问题和解决方案。

* 如果显示以下错误消息：

  ```
  "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  确保密码已使用 `ScrambleUtil` 类。

* 如果显示以下错误消息：

  ```
  "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  确保已在PFX文件中指定了正确的加密密码。

* 如果显示以下错误消息：

  ```
  "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  确保使用密码扰码器类 *参考实施中提供的*. 此Scrambler实用程序与Adobe Primetime DRM Server for Protected Streaming随附的实用程序不同。
