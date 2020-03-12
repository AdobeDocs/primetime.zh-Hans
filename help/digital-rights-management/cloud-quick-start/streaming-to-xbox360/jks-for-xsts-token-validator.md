---
seo-title: 为XSTS验证程序创建JKS
title: 为XSTS验证程序创建JKS
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# 为XSTS验证程序创建JKS{#create-jks-for-an-xsts-validator}

1. 查找位于合作伙伴文件中的私人证书别名 [!DNL .pfx] 名称。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 转换 [!DNL .pfx] 为 [!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (其中 `<alias>` 是您在步骤1中发现的专用证书的别名。)
1. 导入 [!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 放 [!DNL xsts.jks] 入Tomcat主目录，为Tomcat定 `-Dxsts-keystore-password=****` 义。

如果 [!DNL xsts_partner_cert.pfx] 和使 [!DNL xsts.jks] 用的密码不同，请更新中的 `xsts` 密码， `jks` 以使它们相同。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
