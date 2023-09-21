---
title: 获取域CA证书
description: 获取域CA证书
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 获取域CA证书{#obtain-domain-ca-certificates}

与License Server、Packager或Transport证书不同，域CA证书不是由Adobe颁发的。 您可以从证书颁发机构获取此证书，也可以生成自签名证书用于此目的。

域CA证书应使用1024位密钥，并包含CA证书中所需的标准属性：

* CA标志设置为true的基本约束扩展
* 指定允许证书签名的密钥用法扩展

例如，使用OpenSSL，可以生成自签名CA证书，如下所示：

1. 创建名为的文件 [!DNL ca-extensions.txt] 包含：

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. 生成密钥：

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. 生成CSR：

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. 生成证书：

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. 生成密码：

   ```
   openssl rand -base64 8 
   ```

1. 生成PFX：

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```
