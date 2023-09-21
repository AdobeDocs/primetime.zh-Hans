---
title: 疑难解答
description: 疑难解答
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 疑难解答 {#troubleshooting}

下面列出了用于部署的常见问题和解决方案：

* 如果看到以下错误：

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  确保使用提供的对密码进行加密 `ScrambleUtil` 类。

* 如果看到以下错误：

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  确保为PFX文件指定了正确的加密密码。

* 如果看到以下错误：

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  请确保您使用了参考实现中提供的password scrumbler类(此scrumbler实用程序与Adobe® Access™ Server for Protected Streaming中提供的实用程序不同)。
