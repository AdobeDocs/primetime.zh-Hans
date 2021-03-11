---
title: 生成证书签名请求（请求者）
description: 生成证书签名请求（请求者）
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 生成证书签名请求（请求者）{#generate-a-certificate-signing-request-requester}

1. 生成密钥对。 要使用OpenSSL等实用程序，请打开命令窗口并输入以下内容：

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe建议在密钥名中包含证书类型（lic、pkgr、trans、trial或eval）。 此命名规范使您在许可证服务器上部署它们更简单。 此示例使用“mycompany-license.key”。 对于评估版和试用版，请使用“mycompany-eval.key”和“mycompany-trial.key”。

1. 输入密码以保护私钥。

   密码至少应包含12个字符。 字符应包含大小写ASCII字符和数字的混合。 要使用OpenSSL生成强口令，请打开命令窗口并输入以下内容：

   ```
   openssl rand -base64 8
   ```

1. 生成证书签名请求(CSR)。

   要使用OpenSSL生成CSR，请打开命令窗口并输入以下内容：

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. 系统会提示您输入私钥的密码。
1. 创建私钥和密码的备份副本。

   如果您丢失了私钥或私钥已泄露，请与Adobe证书管理员联系以撤销您的证书并请求新证书。

   >[!NOTE]
   >
   >Adobe建议使用HSM保护您的私钥和密码。

