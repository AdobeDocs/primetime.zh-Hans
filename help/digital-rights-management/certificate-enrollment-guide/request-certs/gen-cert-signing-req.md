---
title: 生成证书签名请求（请求者）
description: 生成证书签名请求（请求者）
copied-description: true
exl-id: 4f8dae3d-da56-453d-b3c4-e67fe4f37064
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 生成证书签名请求（请求者） {#generate-a-certificate-signing-request-requester}

1. 生成密钥对。 要使用OpenSSL等实用程序，请打开命令窗口并输入以下内容：

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe建议在密钥名称中包含证书类型（lic、pkgr、trans、trial或eval）。 此命名约定使您在许可证服务器上部署它们时更轻松。 此示例使用“mycompany-license.key”。 对于试用版和评估版，请使用“mycompany-eval.key”和“mycompany-trial.key”。

1. 输入密码以保护私钥。

   密码应至少包含12个字符。 字符应混合使用大写和小写ASCII字符和数字。 要使用OpenSSL生成强密码，请打开命令窗口并输入以下内容：

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

   如果您丢失私钥或私钥已被泄露，请联系Adobe证书管理员以撤销您的证书并申请新证书。

   >[!NOTE]
   >
   >Adobe建议使用HSM来保护您的私钥和密码。
