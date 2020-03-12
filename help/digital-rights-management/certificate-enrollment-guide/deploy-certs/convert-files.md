---
seo-title: 转换文件
title: 转换文件
uuid: e17ee003-5ac2-4bb8-83b7-81ee8fa9ee46
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 转换文件{#convert-files}

请求者使用OpenSSL和私钥等实用程序，通过在命令窗口中输入以下命令来生成PKCS#12(pfx)和PEM/DER文件：

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

1. 将临时PEM文件转换为最终的PEM文件。

   要使用OpenSSL，请打开命令窗口并输入以下内容：

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >尽管不是必需的，Adobe建议对私钥(private_key_password)和PFX(pfx_password)使用不同的口令。

   此最终的PEM文件仅包含您的证书。

1. 将PEM文件转换为DER文件。

   要使用OpenSSL，请打开命令窗口并输入以下内容：

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >DER文件仅对HTTP动态流打包程序是必需的。

