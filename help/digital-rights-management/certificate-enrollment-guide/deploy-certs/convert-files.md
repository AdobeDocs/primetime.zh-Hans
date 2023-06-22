---
title: 转换文件
description: 转换文件
copied-description: true
exl-id: 7344ca2f-5307-403b-a6fc-cbbea7c2829f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 转换文件{#convert-files}

通过使用诸如OpenSSL和私钥之类的实用程序，请求者通过从命令窗口中输入以下命令来生成PKCS#12 (pfx)和PEM/DER文件：

1. 将PKCS#7文件转换为临时PEM文件。

   要使用OpenSSL，请打开命令窗口并输入以下内容：

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >此临时PEM包含您的证书和中间CA的证书。 使用这些证书生成PFX文件。

1. 将临时PEM文件转换为PFX文件。

   要使用OpenSSL，请打开命令窗口并输入以下内容：

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. 将临时PEM文件转换为最终PEM文件。

   要使用OpenSSL，请打开命令窗口并输入以下内容：

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >尽管不是必需的，但Adobe建议对私钥(private_key_password)和PFX (pfx_password)使用不同的口令。

   此最终PEM文件仅包含您的证书。

1. 将PEM文件转换为DER文件。

   要使用OpenSSL，请打开命令窗口并输入以下内容：

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >只有HTTP Dynamic Streaming打包程序才需要DER文件。
