---
title: 为XSTS验证器创建JKS
description: 为XSTS验证器创建JKS
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# 为XSTS验证器创建JKS{#create-jks-for-an-xsts-validator}

1. 了解位于合作伙伴中的私有证书的别名 [!DNL .pfx] 文件。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 转换 [!DNL .pfx] 到 [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (其中 `<alias>` 是您在步骤1中发现的专用证书的别名。)
1. 导入 [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] ，并定义 `-Dxsts-keystore-password=****` 给Tomcat。

如果 [!DNL xsts_partner_cert.pfx] 和 [!DNL xsts.jks] 使用不同的密码，请更新 `xsts` 密码输入 `jks` 让他们变得一样。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
