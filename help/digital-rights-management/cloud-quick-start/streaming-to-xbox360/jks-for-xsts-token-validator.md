---
title: 为XSTS验证程序创建JKS
description: 为XSTS验证程序创建JKS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# 为XSTS validator{#create-jks-for-an-xsts-validator}创建JKS

1. 查找位于伙伴[!DNL .pfx]文件中的私人证书别名。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 将[!DNL .pfx]转换为[!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   （其中`<alias>`是您在步骤1中发现的专用证书的别名。）
1. 导入[!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 将[!DNL xsts.jks]放在Tomcat主目录中，并为Tomcat定义`-Dxsts-keystore-password=****`。

如果[!DNL xsts_partner_cert.pfx]和[!DNL xsts.jks]使用不同的口令，请更新`jks`中的`xsts`口令，使其相同。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
