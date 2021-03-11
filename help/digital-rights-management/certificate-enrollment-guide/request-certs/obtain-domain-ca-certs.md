---
title: 获取域CA证书
description: 获取域CA证书
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 获取域CA证书{#obtain-domain-ca-certificates}

与许可证服务器、包装程序或传输证书不同，域CA证书不是由Adobe颁发的。 您可以从证书颁发机构获得此证书，也可以生成用于此目的的自签名证书。

域CA证书应使用1024位密钥并包含CA证书中所需的标准属性：

* 将CA标志设置为true时的基本约束扩展
* 允许使用指定证书签名的密钥使用扩展

例如，使用OpenSSL，可以生成自签名CA证书，如下所示：

1. 创建名为[!DNL ca-extensions.txt]的文件，其中包含：

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. 生成密钥：

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. 生成CSR:

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

1. 生成PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```

