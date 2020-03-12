---
seo-title: 疑难解答
title: 疑难解答
uuid: db76d6a4-c285-4d86-95a1-4f1a85ed3743
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 疑难解答 {#troubleshooting}

下面列出了部署的常见问题和解决方案：

* 如果您看到以下错误：

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   确保使用提供的类加密密 `ScrambleUtil` 码。

* 如果您看到以下错误：

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   确保为PFX文件指定了正确的加密密码。

* 如果您看到以下错误：

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   确保使用了随“参考实施”提供的口令扰码器类（此扰码器实用程序与随“Adobe® Access™ Server for Protected Streaming”提供的类不同）。

